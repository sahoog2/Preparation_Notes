# **Multithreading in Java & The `Thread` Class**

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

### **Java `Thread` Class**

The `Thread` class is Java’s built-in way to create and manage threads.

#### **1️⃣ Creating a Thread by Extending `Thread` Class**

```java
class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("Thread running: " + Thread.currentThread().getName());
    }
}

public class ThreadExample {
    public static void main(String[] args) {
        MyThread thread1 = new MyThread();
        MyThread thread2 = new MyThread();

        thread1.start();  // Starts thread execution
        thread2.start();
    }
}

```

🛠 **Key Points**

-   `start()` creates a new thread.
-   `run()` contains the execution logic.
-   Threads execute **asynchronously**, meaning output order may vary.

----------


### **Thread Lifecycle**

Threads go through several states during execution:

1.  **New** – Created but not started.
2.  **Runnable** – Ready to run, waiting for CPU allocation.
3.  **Running** – Actively executing.
4.  **Blocked/Waiting** – Paused due to synchronization or waiting for resources.
5.  **Terminated** – Execution completed.

----------


### **✅ Example: Creating Threads Using `Thread` Class**

This example **simulates downloading files** using multiple threads.

```java
class DownloadTask extends Thread {
    private String fileName;

    public DownloadTask(String fileName) {
        this.fileName = fileName;
    }

    @Override
    public void run() {
        System.out.println("Downloading " + fileName + " by " + Thread.currentThread().getName());
        try {
            Thread.sleep(2000); // Simulating download time
        } catch (InterruptedException e) {
            System.out.println("Download interrupted for " + fileName);
        }
        System.out.println("Download completed: " + fileName);
    }
}

public class ThreadExample {
    public static void main(String[] args) {
        DownloadTask thread1 = new DownloadTask("File1.pdf");
        DownloadTask thread2 = new DownloadTask("File2.jpg");
        DownloadTask thread3 = new DownloadTask("File3.mp4");

        thread1.start();
        thread2.start();
        thread3.start();
    }
}

```

----------

### **🛠 Explanation**

✔ **Extending `Thread` Class:** We define a custom thread by extending `Thread`.  
✔ **Overriding `run()` Method:** Logic inside `run()` executes when the thread starts.  
✔ **Using `start()` Method:** Starts each thread asynchronously.  
✔ **`Thread.sleep(2000)` Simulates Work:** The thread pauses for 2 seconds to mimic processing.  
✔ **`Thread.currentThread().getName()` Identifies Threads:** Useful for debugging.

----------

### **🛠 Sample Output**

```
Downloading File1.pdf by Thread-0
Downloading File2.jpg by Thread-1
Downloading File3.mp4 by Thread-2
Download completed: File1.pdf
Download completed: File2.jpg
Download completed: File3.mp4

```

# **Multithreading Using `Executor` – Concrete Example**

In Java, the `Executor` framework allows efficient **thread management** without manually creating and starting threads. This improves performance and scalability.

----------

### **✅ Example: Using `Executor` for Multithreading**

This example **simulates processing multiple database queries** using an `Executor`.

```java
import java.util.concurrent.Executor;
import java.util.concurrent.Executors;

class DatabaseTask implements Runnable {
    private String query;

    public DatabaseTask(String query) {
        this.query = query;
    }

    @Override
    public void run() {
        System.out.println("Executing query: " + query + " by " + Thread.currentThread().getName());
    }
}

public class ExecutorExample {
    public static void main(String[] args) {
        Executor executor = Executors.newFixedThreadPool(3); // Creates a thread pool of 3 threads
        
        executor.execute(new DatabaseTask("SELECT * FROM users"));
        executor.execute(new DatabaseTask("DELETE FROM logs"));
        executor.execute(new DatabaseTask("UPDATE accounts SET balance = balance + 100"));
        
        executor.execute(new DatabaseTask("INSERT INTO transactions VALUES ('TX123', 5000)"));
    }
}

```

----------

### **🛠 Explanation**

✔ **Using `Executor`** – Defines a fixed-size thread pool.  
✔ **Avoids Manual Thread Management** – No need for `new Thread()`.  
✔ **`execute()` Method** – Efficiently runs tasks asynchronously.  
✔ **Thread Pooling** – Reuses threads to execute tasks faster.

🛠 **Expected Output** (Order may vary due to concurrency):

```
Executing query: SELECT * FROM users by pool-1-thread-1
Executing query: DELETE FROM logs by pool-1-thread-2
Executing query: UPDATE accounts SET balance = balance + 100 by pool-1-thread-3
Executing query: INSERT INTO transactions VALUES ('TX123', 5000) by pool-1-thread-1

```

----------

Great! Let's dive into **ExecutorService**, which provides advanced thread management in Java.

----------
# **Multithreading Using `ExecutorService` 
### **What is `ExecutorService`?**

`ExecutorService` is an enhanced version of `Executor` that: ✔ Allows **efficient execution of multiple tasks** using thread pools.  
✔ Supports **task submission and lifecycle management** (start, shutdown).  
✔ Enables **control over thread execution**, unlike basic `Executor`.

----------

### **✅ Example: Using `ExecutorService` for Thread Pool Management**

This example **simulates processing multiple transactions** using `ExecutorService`.

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

class TransactionTask implements Runnable {
    private String transactionId;

    public TransactionTask(String transactionId) {
        this.transactionId = transactionId;
    }

    @Override
    public void run() {
        System.out.println("Processing transaction: " + transactionId + " by " + Thread.currentThread().getName());
    }
}

public class ExecutorServiceExample {
    public static void main(String[] args) {
        ExecutorService executorService = Executors.newFixedThreadPool(3); // Creates a pool with 3 threads

        for (int i = 1; i <= 5; i++) {
            executorService.submit(new TransactionTask("TX" + i));
        }

        executorService.shutdown(); // Gracefully shuts down the thread pool
    }
}

```

----------

### **🛠 Explanation**

✔ **Fixed Thread Pool (`Executors.newFixedThreadPool(3)`)** – Uses 3 threads for execution.  
✔ **Task Submission (`submit()`)** – Adds multiple transactions for processing.  
✔ **Graceful Shutdown (`shutdown()`)** – Ensures proper resource cleanup.

----------

### **🛠 Sample Output**

```
Processing transaction: TX1 by pool-1-thread-1
Processing transaction: TX2 by pool-1-thread-2
Processing transaction: TX3 by pool-1-thread-3
Processing transaction: TX4 by pool-1-thread-1
Processing transaction: TX5 by pool-1-thread-2

```

🔹 **Thread pool reuses existing threads**, avoiding excessive creation overhead.

----------

### **✅ Advanced Control: `shutdown()` vs. `shutdownNow()`**

```java
executorService.shutdown(); // Waits for tasks to finish before shutting down
executorService.shutdownNow(); // Immediately stops active tasks

```

Great choice! Let's dive into **`Callable` and `Future`**, which allow threads to return results asynchronously.

----------
# **Multithreading Using Callable
### **✅ What is `Callable`?**

Unlike `Runnable`, `Callable<T>`: ✔ Can **return a value** from a thread.  
✔ Can **throw checked exceptions**.  
✔ Works with `Future<T>` for **asynchronous processing**.

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
