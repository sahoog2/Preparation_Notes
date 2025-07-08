[Solution](#SOLUTION)  [Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25475/homework/problems/64/hints?navref=cl_pb_nv_tb)  [Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Sorting/002%20problems.md)

Q1.  Largest Number

**Problem Description**  
Given an array  **A**  of non-negative integers, arrange them such that they form the largest number.

**Note:**  The result may be very large, so you need to return a string instead of an integer.

**Problem Constraints**  
1 <= len(A) <= 100000  
0 <= A[i] <= 2*109
 
**Input Format**  
The first argument is an array of integers.
  
**Output Format**  
Return a string representing the largest number.

  
  
**Example Input**  
Input 1:
 A = [3, 30, 34, 5, 9]
 
Input 2:
 A = [2, 3, 9, 0]

**Example Output**  
Output 1:
 "9534330"
 
Output 2:
 "9320" 
  
**Example Explanation**  
Explanation 1:
Reorder the numbers to [9, 5, 34, 3, 30] to form the largest number.

Explanation 2:
Reorder the numbers to [9, 3, 2, 0] to form the largest number 9320.

# SOLUTION

``` java
public class Solution {
    public String largestNumber(int[] A) {
        Integer[] arr = Arrays.stream(A).boxed().toArray(Integer[]::new);
        Arrays.sort(arr, (a, b) -> (b + "" + a).compareTo(a + "" + b));

        if (arr[0] == 0) return "0"; // Handle case like [0, 0]

        StringBuilder sb = new StringBuilder();
        for (int num : arr) sb.append(num);

        return sb.toString();


    }
}

```

Let's break down the logic of this `largestNumber` method step by step. The goal is to **arrange the integers in an order such that they form the largest possible number** when concatenated.

---

### ✅ Step-by-Step Explanation

#### 🔹 1. Convert `int[]` to `Integer[]`
```java
Integer[] arr = Arrays.stream(A).boxed().toArray(Integer[]::new);
```
- **Why?** Sorting with a custom comparator requires objects, not primitives.
- `boxed()` converts `int` primitives to `Integer` objects.
- `toArray(Integer[]::new)` creates an actual `Integer[]`.

---

#### 🔹 2. Custom Sort Using Comparator
```java
Arrays.sort(arr, (a, b) -> (b + "" + a).compareTo(a + "" + b));
```
- This comparator ensures that two numbers `a` and `b` are ordered based on the value of **`b+a` vs `a+b`**.
- Example:
  - For `a = 9`, `b = 34`:
    - `b+a = "349"`, `a+b = "934"` ⇒ `"934"` > `"349"` ⇒ So place `9` before `34`.
- This ensures the **maximum number** is formed by concatenation.

---

#### 🔹 3. Handle Leading Zeros Edge Case
```java
if (arr[0] == 0) return "0";
```
- If the largest number starts with `0`, then the entire number is `0` (i.e., input was `[0, 0, 0]`).
- This avoids returning `"000"` and instead correctly returns `"0"`.

---

#### 🔹 4. Build the Final Result
```java
StringBuilder sb = new StringBuilder();
for (int num : arr) sb.append(num);
return sb.toString();
```
- Appends the numbers (in descending order) to form the final result string.

---

### 🧪 Example Input
```java
int[] A = {3, 30, 34, 5, 9};
```

### ✅ Sorted Order
```java
[9, 5, 34, 3, 30]
```

### ✅ Final Output
```java
"9534330"
```

---


[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Sorting/002%20problems.md)
