# **Multithreading in Java

#### **What is Multithreading?**

Multithreading is the ability of a program to execute multiple threads **simultaneously**, allowing tasks to be performed concurrently. This improves **performance** and **responsiveness**, especially in applications that involve heavy computations or I/O operations.

-   **Thread**: A lightweight subprocess that executes independently.
-   **Multithreading**: Running multiple threads simultaneously within a single Java application.

----------

### **Advantages of Multithreading**

✔ **Efficient CPU Utilization** – Multiple threads execute independently.  
✔ **Non-blocking Operations** – Ideal for applications that need smooth UI interactions.  
✔ **Faster Execution** – Threads reduce waiting time by running parallel tasks.  
✔ **Better Resource Sharing** – Threads share memory space, reducing overhead.

----------
# Runnable vs Callable

### **Runnable vs. Callable in Java**

Both `Runnable` and `Callable` are **functional interfaces** used in Java for multithreading. However, they serve **different purposes**.

----------

### **✅ Key Differences**

| Feature | Runnable |Callable
|--|--|--|
| **Return Value** |**Does not return a result** (`void run()`)  |**Returns a result** (`T call()`)
|**Checked Exceptions**|**Cannot throw checked exceptions**|**Can throw checked exceptions**
|**Use Case**|When you need a task **without a return value**|When you need a task **with a return value**
|**Integration**|Works with `Thread` & `Executor`|Works with `ExecutorService`

----------

### **✅ Example 1: `Runnable` (No Return Value)**

```java
class PrintTask implements Runnable {
    @Override
    public void run() {
        System.out.println("Executing Runnable in thread: " + Thread.currentThread().getName());
    }
}

public class RunnableExample {
    public static void main(String[] args) {
        Thread thread = new Thread(new PrintTask());
        thread.start();
    }
}

```

✔ **Best for executing tasks that don't require a return value**.

----------

### **✅ Example 2: `Callable` (Returns a Value)**

```java
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

class TaskWithResult implements Callable<String> {
    @Override
    public String call() {
        return "Task completed by " + Thread.currentThread().getName();
    }
}

public class CallableExample {
    public static void main(String[] args) throws Exception {
        ExecutorService executor = Executors.newFixedThreadPool(2);
        Future<String> future = executor.submit(new TaskWithResult());

        System.out.println("Result: " + future.get()); // Retrieves the result
        executor.shutdown();
    }
}

```

✔ **Best for executing tasks that require a return value**.  
✔ **Uses `Future` to retrieve the result asynchronously**.

----------

### **🚀 When to Use `Runnable` vs. `Callable`?**

-   **Use `Runnable`** when the task **doesn't need a return value** (e.g., logging, sending notifications).
-   **Use `Callable`** when the task **needs to return a result** (e.g., fetching data from a database).

# Implementing Runnable using Thread
Below is a **concrete example** of using a `Thread` to execute a `Runnable` task in Java.


### **✅ Example: Running a Task Using `Runnable` with `Thread`**

This example **simulates processing multiple payment transactions** using `Runnable`.

```java
class PaymentProcessor implements Runnable {
    private String transactionId;

    public PaymentProcessor(String transactionId) {
        this.transactionId = transactionId;
    }

    @Override
    public void run() {
        System.out.println("Processing transaction: " + transactionId + " - Thread: " + Thread.currentThread().getName());
        try {
            Thread.sleep(2000); // Simulating transaction delay
        } catch (InterruptedException e) {
            System.out.println("Transaction interrupted for: " + transactionId);
        }
        System.out.println("Transaction completed: " + transactionId);
    }
}

public class RunnableThreadExample {
    public static void main(String[] args) {
        Thread thread1 = new Thread(new PaymentProcessor("TXN001"));
        Thread thread2 = new Thread(new PaymentProcessor("TXN002"));
        Thread thread3 = new Thread(new PaymentProcessor("TXN003"));

        thread1.start();
        thread2.start();
        thread3.start();
    }
}

```

----------

### **🛠 Explanation**

✔ **Uses `Runnable` for Task Definition** – `PaymentProcessor` implements `Runnable`.  
✔ **Passes `Runnable` to `Thread` Constructor** – Creates threads dynamically.  
✔ **Executes Tasks Concurrently (`start()`)** – Multiple transactions processed in parallel.  
✔ **Simulates Processing Delay (`Thread.sleep(2000)`)** – Adds realism to execution time.  
✔ **Uses `Thread.currentThread().getName()`** – Helps track which thread is executing the task.

----------

### **🛠 Expected Output (Order may vary due to concurrency)**

```
Processing transaction: TXN001 - Thread: Thread-0
Processing transaction: TXN002 - Thread: Thread-1
Processing transaction: TXN003 - Thread: Thread-2
Transaction completed: TXN001
Transaction completed: TXN002
Transaction completed: TXN003

```

🔹 **Each transaction is handled by a separate thread**, demonstrating multithreading with `Runnable`.

# Implementing Runnable using Executor
Below is a **concrete example** of using `Executor` to execute `Runnable` tasks efficiently in Java.


### **✅ Example: Using `Executor` to Process Tasks in Parallel**

This example **simulates logging multiple user actions using an `Executor`**.

```java
import java.util.concurrent.Executor;
import java.util.concurrent.Executors;

class UserActionLogger implements Runnable {
    private String action;

    public UserActionLogger(String action) {
        this.action = action;
    }

    @Override
    public void run() {
        System.out.println("Logging action: " + action + " - Thread: " + Thread.currentThread().getName());
    }
}

public class ExecutorRunnableExample {
    public static void main(String[] args) {
        Executor executor = Executors.newFixedThreadPool(3); // Creates a pool with 3 threads

        executor.execute(new UserActionLogger("Login"));
        executor.execute(new UserActionLogger("File Upload"));
        executor.execute(new UserActionLogger("Logout"));
        executor.execute(new UserActionLogger("Profile Update"));
    }
}

```

----------

### **🛠 Explanation**

✔ **Uses `Executor` to manage threads efficiently.**  
✔ **Creates a thread pool (`Executors.newFixedThreadPool(3)`)** – Reuses threads instead of creating new ones each time.  
✔ **Submits tasks using `execute()`** – Executes `Runnable` without manual thread handling.  
✔ **Identifies executing thread (`Thread.currentThread().getName()`)** – Useful for debugging.

----------

### **🛠 Expected Output**

```
Logging action: Login - Thread: pool-1-thread-1
Logging action: File Upload - Thread: pool-1-thread-2
Logging action: Logout - Thread: pool-1-thread-3
Logging action: Profile Update - Thread: pool-1-thread-1

```

🔹 **Threads are reused** across tasks for efficiency.

# Implementing Runnable using ExecutorService
### **Concrete Example: Using `ExecutorService` for Running `Runnable` Tasks**

`ExecutorService` is an advanced thread management framework in Java that helps execute multiple tasks efficiently using thread pools.

----------

### **✅ Example: Processing Multiple File Uploads Using `ExecutorService`**

This example **simulates multiple file uploads being handled concurrently**.

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

class FileUploader implements Runnable {
    private String fileName;

    public FileUploader(String fileName) {
        this.fileName = fileName;
    }

    @Override
    public void run() {
        System.out.println("Uploading file: " + fileName + " - Thread: " + Thread.currentThread().getName());
        try {
            Thread.sleep(2000); // Simulating file upload delay
        } catch (InterruptedException e) {
            System.out.println("Upload interrupted for: " + fileName);
        }
        System.out.println("Upload completed: " + fileName);
    }
}

public class ExecutorServiceExample {
    public static void main(String[] args) {
        ExecutorService executorService = Executors.newFixedThreadPool(3); // Creates a pool with 3 threads

        executorService.execute(new FileUploader("document.pdf"));
        executorService.execute(new FileUploader("video.mp4"));
        executorService.execute(new FileUploader("image.jpg"));
        executorService.execute(new FileUploader("audio.mp3"));

        executorService.shutdown(); // Gracefully shuts down the thread pool
    }
}

```

----------

### **🛠 Explanation**

✔ **Uses `ExecutorService` for Efficient Thread Management** – Avoids manual thread handling.  
✔ **Creates a Fixed Thread Pool (`Executors.newFixedThreadPool(3)`)** – Allows **3 threads** to run at a time.  
✔ **Executes `Runnable` Tasks Using `execute()`** – Runs tasks asynchronously.  
✔ **Uses `shutdown()`** – Ensures proper cleanup after execution.

----------

### **🛠 Expected Output (Order may vary due to concurrency)**

```
Uploading file: document.pdf - Thread: pool-1-thread-1
Uploading file: video.mp4 - Thread: pool-1-thread-2
Uploading file: image.jpg - Thread: pool-1-thread-3
Uploading file: audio.mp3 - Thread: pool-1-thread-1
Upload completed: document.pdf
Upload completed: video.mp4
Upload completed: image.jpg
Upload completed: audio.mp3

```

🔹 **Threads are reused**, improving efficiency.
Awesome! Let's dive into **`Callable` & `Future`**, which allow threads to return results asynchronously.

----------
# Implementing multithreading using Callable
### **✅ What is `Callable`?**

Unlike `Runnable`, `Callable<T>`: ✔ **Returns a value** from a thread.  
✔ **Throws checked exceptions**.  
✔ **Works with `Future<T>`** for **asynchronous result retrieval**.

🔹 **Key difference between `Runnable` and `Callable`:**

```java
@FunctionalInterface
public interface Runnable {
    void run(); // No return value
}

@FunctionalInterface
public interface Callable<V> {
    V call() throws Exception; // Returns value
}

```

----------

### **✅ Example: Using `Callable` & `Future` in `ExecutorService`**

This example **simulates fetching user details asynchronously**.

```java
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

class UserFetcher implements Callable<String> {
    private String userId;

    public UserFetcher(String userId) {
        this.userId = userId;
    }

    @Override
    public String call() throws Exception {
        Thread.sleep(2000); // Simulating database fetch delay
        return "User details for ID: " + userId;
    }
}

public class CallableExample {
    public static void main(String[] args) throws Exception {
        ExecutorService executorService = Executors.newFixedThreadPool(2);

        Future<String> future = executorService.submit(new UserFetcher("12345"));

        System.out.println("Fetching user asynchronously...");
        
        String userDetails = future.get(); // Blocks until result is available
        System.out.println("Result: " + userDetails);
        
        executorService.shutdown();
    }
}

```

----------

### **🛠 Explanation**

✔ **Using `Callable` to Return Values** – Unlike `Runnable`, `call()` can return results.  
✔ **Submitting Task with `Future`** – Used to retrieve asynchronous execution results.  
✔ **`future.get()` Blocks Until Task Completes** – Ensures result retrieval.  
✔ **Graceful Shutdown (`shutdown()`)** – Cleans up the thread pool after execution.

----------

### **🛠 Expected Output**

```
Fetching user asynchronously...
(Result appears after 2 seconds)
Result: User details for ID: 12345

```

🔹 The program **does not block** while the task executes—enhancing efficiency.

----------

# `CompletableFuture` for Advanced Asynchronous Programming.

Let's explore **`CompletableFuture`**, which enables **fully asynchronous programming** in Java.

----------

### **✅ What is `CompletableFuture`?**

`CompletableFuture<T>` extends `Future<T>` and provides: ✔ **Non-blocking execution** – Unlike `Future.get()`, which blocks execution.  
✔ **Chaining operations** – Supports multiple asynchronous steps (`thenApply`, `thenAccept`).  
✔ **Error handling** – Provides mechanisms like `exceptionally()` and `handle()`.

----------

### **✅ Example: Using `CompletableFuture` for Asynchronous Execution**

This example **simulates fetching user details asynchronously without blocking the main thread**.

```java
import java.util.concurrent.CompletableFuture;

public class CompletableFutureExample {
    public static void main(String[] args) {
        System.out.println("Fetching user asynchronously...");

        CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
            try {
                Thread.sleep(2000); // Simulating database fetch delay
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            return "User details for ID: 12345";
        });

        future.thenAccept(result -> System.out.println("Result: " + result));

        System.out.println("Main thread continues executing...");
        
        future.join(); // Waits for result without blocking other operations
    }
}

```

----------

### **🛠 Explanation**

✔ **Uses `supplyAsync()` to Fetch Data Asynchronously** – Executes in a separate thread.  
✔ **Attaches `thenAccept()` for Non-blocking Callbacks** – Processes result once available.  
✔ **Main Thread Continues Execution** – Avoids blocking while waiting for data.  
✔ **Uses `join()` for Graceful Completion** – Ensures cleanup without blocking execution.

----------

### **🛠 Expected Output**

```
Fetching user asynchronously...
Main thread continues executing...
(Result appears after 2 seconds)
Result: User details for ID: 12345

```

🔹 Unlike `Future.get()`, `CompletableFuture` **does not block** execution.

----------

# ✅  `thenCombine()` and `exceptionally()` for Advanced Chaining and Error Handling


### **✅ Using `thenCombine()` to Combine Multiple Async Tasks**

When you need to **combine results from two independent async tasks**, `thenCombine()` is ideal.

```java
import java.util.concurrent.CompletableFuture;

public class CompletableFutureCombineExample {
    public static void main(String[] args) {
        CompletableFuture<Integer> future1 = CompletableFuture.supplyAsync(() -> {
            System.out.println("Fetching product price...");
            return 200;
        });

        CompletableFuture<Integer> future2 = CompletableFuture.supplyAsync(() -> {
            System.out.println("Fetching delivery charges...");
            return 50;
        });

        CompletableFuture<Integer> finalPrice = future1.thenCombine(future2, (price, delivery) -> price + delivery);

        System.out.println("Total Price: " + finalPrice.join());
    }
}

```

🛠 **Expected Output:**

```
Fetching product price...
Fetching delivery charges...
Total Price: 250

```

✔ **Executes tasks asynchronously**.  
✔ **Combines results when both tasks complete**.

----------

### **✅ Using `exceptionally()` for Error Handling**

`exceptionally()` helps **gracefully handle errors** and provide fallback values.

```java
import java.util.concurrent.CompletableFuture;

public class CompletableFutureExceptionHandling {
    public static void main(String[] args) {
        CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
            if (Math.random() > 0.5) throw new RuntimeException("Error fetching data!");
            return "Fetched user details";
        }).exceptionally(ex -> "Fallback data due to error");

        System.out.println("Result: " + future.join());
    }
}

```

✔ **Handles runtime exceptions elegantly**.  
✔ **Provides fallback data instead of crashing**.


#  **`thenCompose()`**, which is used when one asynchronous task depends on another.

----------

### **✅ What is `thenCompose()`?**

✔ **Chains dependent async calls** – Similar to flat-mapping in functional programming.  
✔ **Prevents nested `CompletableFuture` instances** – Returns a single `CompletableFuture<T>`.  
✔ **Useful for scenarios where one async task requires another's result**.

----------

### **✅ Example: Fetching User Data and Then Their Orders**

This example **first fetches user details, then fetches their order history asynchronously**.

```java
import java.util.concurrent.CompletableFuture;

public class CompletableFutureComposeExample {
    public static CompletableFuture<String> getUserData(String userId) {
        return CompletableFuture.supplyAsync(() -> "User: " + userId);
    }

    public static CompletableFuture<String> getOrdersForUser(String user) {
        return CompletableFuture.supplyAsync(() -> "Orders for " + user + " → [Order1, Order2, Order3]");
    }

    public static void main(String[] args) {
        CompletableFuture<String> future = getUserData("12345")
            .thenCompose(user -> getOrdersForUser(user)); // Uses the user's data to fetch their orders

        System.out.println("Fetching user orders...");
        System.out.println("Result: " + future.join());
    }
}

```

----------

### **🛠 Expected Output**

```
Fetching user orders...
Result: Orders for User: 12345 → [Order1, Order2, Order3]

```

✔ **Avoids unnecessary nesting (`thenApply()` would return `CompletableFuture<CompletableFuture<T>>`).**  
✔ **Ensures proper chaining when one async task depends on another.**
