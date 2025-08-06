## 🔧 **What is Sorting?**

Sorting is the process of arranging data in a particular format—usually in **ascending or descending order**. Efficient sorting is crucial in:

-   Searching algorithms (like binary search)
-   Data visualization
-   Database query optimization
-   Interview challenges and competitive programming

----------

## 📚 **Classification of Sorting Algorithms**


Sorting algorithms can be classified in several ways based on their behavior, efficiency, and characteristics. Here's a structured overview:

----------

#### 📊 **Classification of Sorting Algorithms**

##### 1. 🔍 **Based on Comparison**

-   **Comparison-Based Sorting**: Elements are sorted by comparing them.
    -   Examples: Bubble Sort, Selection Sort, Insertion Sort, Merge Sort, Quick Sort, Heap Sort
-   **Non-Comparison-Based Sorting**: Sorting is done without direct comparisons.
    -   Examples: Counting Sort, Radix Sort, Bucket Sort  
        [Learn more about this classification](https://www.wscubetech.com/resources/dsa/sorting-algorithms)

----------

##### 2. 🔁 **Based on Recursion**

-   **Recursive Algorithms**: Use recursion to divide and conquer.
    -   Examples: Merge Sort, Quick Sort
-   **Non-Recursive Algorithms**: Use iterative logic.
    -   Examples: Bubble Sort, Selection Sort, Insertion Sort

----------

##### 3. ⚖️ **Based on Stability**

-   **Stable Sorting**: Preserves the relative order of equal elements.
    -   Examples: Bubble Sort, Merge Sort, Insertion Sort, Counting Sort
-   **Unstable Sorting**: May change the relative order of equal elements.
    -   Examples: Quick Sort, Heap Sort, Selection Sort

----------

##### 4. 🧠 **Based on Adaptability**

-   **Adaptive Sorting**: Performance improves with partially sorted input.
    -   Examples: Insertion Sort, Bubble Sort, Quick Sort
-   **Non-Adaptive Sorting**: Performance remains the same regardless of input order.
    -   Examples: Selection Sort, Merge Sort, Heap Sort

----------

##### 5. 🧮 **Based on Memory Usage**

-   **In-Place Sorting**: Uses minimal extra space (O(1)).
    -   Examples: Quick Sort, Heap Sort, Bubble Sort
-   **Out-of-Place Sorting**: Requires additional memory.
    -   Examples: Merge Sort, Counting Sort, Radix Sort

----------

##### 6. 💾 **Based on Data Location**

-   **Internal Sorting**: Operates entirely in main memory.
    -   Examples: Quick Sort, Bubble Sort
-   **External Sorting**: Uses external storage (e.g., disk) for large datasets.
    -   Example: External Merge Sort  
        [Explore more types and examples](https://prepinsta.com/classification-of-sorting-algorithms/)

----------

## 🔢 **Common Sorting Algorithms**

### 1️⃣ **Bubble Sort** – Simple but Inefficient

**Time Complexity:**

-   Best: O(n) | Avg/Worst: O(n²)  
    **Space:** O(1)  
    **Stable:** ✅

```java
for (int i = 0; i < arr.length - 1; i++) {
    for (int j = 0; j < arr.length - i - 1; j++) {
        if (arr[j] > arr[j + 1]) {
            int temp = arr[j];
            arr[j] = arr[j + 1];
            arr[j + 1] = temp;
        }
    }
}

```

----------

### 2️⃣ **Selection Sort** – Always O(n²)

**Time Complexity:** O(n²) for all cases  
**Space:** O(1)  
**Stable:** ❌

```java
for (int i = 0; i < arr.length - 1; i++) {
    int min = i;
    for (int j = i + 1; j < arr.length; j++) {
        if (arr[j] < arr[min]) {
            min = j;
        }
    }
    int temp = arr[min];
    arr[min] = arr[i];
    arr[i] = temp;
}

```

----------

### 3️⃣ **Insertion Sort** – Efficient for Small/Nearly Sorted Arrays

**Time Complexity:** Best: O(n), Worst: O(n²)  
**Space:** O(1)  
**Stable:** ✅

```java
for (int i = 1; i < arr.length; i++) {
    int key = arr[i];
    int j = i - 1;
    while (j >= 0 && arr[j] > key) {
        arr[j + 1] = arr[j];
        j--;
    }
    arr[j + 1] = key;
}

```

----------

### 4️⃣ **Merge Sort** – Divide & Conquer

**Time Complexity:** O(n log n)  
**Space:** O(n)  
**Stable:** ✅

```java
void mergeSort(int[] arr, int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }
}

```

----------

### 5️⃣ **Quick Sort** – Fast but Worst Case is O(n²)

**Time Complexity:** Best/Average: O(n log n) | Worst: O(n²)  
**Space:** O(log n) (recursive stack)  
**Stable:** ❌

```java
int partition(int[] arr, int low, int high) {
    int pivot = arr[high];
    int i = low - 1;
    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            int temp = arr[i]; arr[i] = arr[j]; arr[j] = temp;
        }
    }
    int temp = arr[i + 1]; arr[i + 1] = arr[high]; arr[high] = temp;
    return i + 1;
}

```

----------

### 6️⃣ **Heap Sort** – Uses Max-Heap

**Time Complexity:** O(n log n)  
**Space:** O(1)  
**Stable:** ❌  
Used where in-place and non-recursive sort is needed.

----------

### 7️⃣ **Counting Sort** – For Known Small Ranges

**Time Complexity:** O(n + k)  
**Space:** O(k)  
**Stable:** ✅  
Only works with **non-negative integers** and known small range.

----------

### 8️⃣ **Radix Sort** – For Integers/Digits

**Time Complexity:** O(nk) (k = # digits)  
**Stable:** ✅  
Great for sorting IDs, phone numbers, etc.

----------

## 📊 Comparison Summary
| Algorithm | Time Complexity (Avg) |Space|Stable|In-place|
|--|--|--|--|--|
| Bubble Sort | O(n²) |O(1)|✅|✅|
|Selection Sort|O(n²) |O(1)|❌|✅|
|Insertion Sort|O(n²) |O(1)|✅|✅|
|Merge Sort|O(nlogn)|O(n)|✅|❌|
|Quick Sort|O(nlogn)|O(logn)|❌|✅|
|Heap Sort|O(nlogn)|O(1)|❌|✅|
|Counting Sort|O(n+k)|O(k)|✅|❌|
|Radix Sort|O(nk)|O(n+k)|✅|❌|

----------

## 🧠 When to Use What?
| Scenario | Recommended Sort |
|--|--|
| Small array|Insertion Sort|
 |Large unsorted data  |Merge or Quick Sort|
 |Sorted/Almost sorted|Insertion Sort|
 |Limited integer range|Counting or Radix Sort|
 |Parallel sort needed|Merge Sort|
 |In-place, no stability|Quick or Heap Sort|


<pre>
Start
  |
  |-- Is the dataset tiny (n < 10)?
  |       |-- Yes --> Insertion Sort
  |       |-- No --> Continue
  |
  |-- Need stable sort?
  |       |-- Yes
  |       |    |-- Is data size large? 
  |       |          |-- Yes --> Merge Sort
  |       |          |-- No  --> Insertion Sort
  |       |-- No
  |            |-- Are space constraints tight?
  |                  |-- Yes --> Heap Sort
  |                  |-- No
  |                        |-- Is average case speed critical?
  |                              |-- Yes --> Quick Sort
  |                              |-- No  --> Selection Sort

</pre>



