#  Closest MinMax

[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25458/assignment/problems/986/hints?navref=cl_pb_nv_tb)
[Solution](#Solution)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
[Attempts](#Attempts)


**Problem Description**  

Given an array  **A**, find the size of the smallest subarray such that it contains at least one occurrence of the maximum value of the array and at least one occurrence of the minimum value of the array.

  
  
**Problem Constraints**  

1 <=  **|A|**  <= 2000

  
  
**Input Format**  

First and only argument is vector  **A**

  
  
**Output Format**  

Return the length of the smallest subarray which has at least one occurrence of minimum and maximum element of the array

  
  
**Example Input**  

Input 1:

A = [1, 3, 2]

Input 2:

A = [2, 6, 1, 6, 9]

  
  
**Example Output**  

Output 1:

 2

Output 2:

 3

  
  
**Example Explanation**  

Explanation 1:

 Take the 1st and 2nd elements as they are the minimum and maximum elements respectievly.

Explanation 2:

 Take the last 3 elements of the array.

[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25458/assignment/problems/986/hints?navref=cl_pb_nv_tb)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)

# Solution

This problem can be solved in a simple O(N) complexity.  
We can implement a sliding window kind of algorithm using two pointers. We can slide over the array and keep track of every last occurrence of the minimum and maximum element of the array.  
In order to find the start point, we can simply remember the last occurrences of a minimum and a maximum value, respectively. And for each min-max pair, we check the length of the subarray that encloses them and then update out overall based on that.

**Time Complexity : O(n)**  
**Space Complexity(extra) : O(1)**

```java
My incorrect Solution :

    for(int i=0;i<A.length;i++){
        if(A[i]<=min_val){
            min_idex = i;
            min_val = A[i];
        }
        if(A[i]>=max_val){
            max_index =i;
            max_val = A[i];
        }
        ans = Math.min(ans, Math.abs(max_index-min_idex));
    }

    return ans;
}
```
[Corrected Approach](#-corrected-approach)

### **Logical Error in the Given Solution**
The **mistake** in the current approach is that it **does not correctly track the latest occurrences** of the **minimum and maximum values** in the array while iterating. This leads to **incorrect results** when the min/max values appear multiple times.

#### **🚨 Error Explanation**
- The variables `min_index` and `max_index` are **updated only when a new min/max value appears**.
- However, this incorrectly ignores **previous occurrences of min/max** that could form a smaller subarray.
- `ans` is updated on **every iteration**, even when one of the values is not found **after** the other.

---

### **❌ Counterexample Where It Fails**
Consider the array:
```java
A = [1, 3, 2, 1, 3, 3, 1]
```
- **Min value:** `1`
- **Max value:** `3`
- Correct answer should be `2` (`[3, 1]` at indices `4,5`).
- **Incorrect output:** The function incorrectly updates `min_index` when encountering `1` later, missing a smaller subarray.

---

### **✅ Corrected Approach**
We should **track** both the latest occurrence of `min` and `max` as we iterate, ensuring we always have the shortest subarray.

```java
public class Solution {
    public int solve(int[] A) {
        int min_val = Integer.MAX_VALUE;
        int max_val = Integer.MIN_VALUE;

        // Find actual min and max values first
        for (int num : A) {
            min_val = Math.min(min_val, num);
            max_val = Math.max(max_val, num);
        }

        int min_index = -1, max_index = -1;
        int ans = Integer.MAX_VALUE;

        // Iterate and track closest min-max occurrences
        for (int i = 0; i < A.length; i++) {
            if (A[i] == min_val) {
                min_index = i;
                if (max_index != -1) { // Ensure max exists before
                    ans = Math.min(ans, i - max_index + 1);
                }
            }
            if (A[i] == max_val) {
                max_index = i;
                if (min_index != -1) { // Ensure min exists before
                    ans = Math.min(ans, i - min_index + 1);
                }
            }
        }
        return ans;
    }
}
```

---

### **🔥 Why This Works?**
✅ First **identify min and max values** in the array.  
✅ Track the **latest occurrence** of both min and max values.  
✅ Ensure that when updating `ans`, **both values have been seen** before updating.  

This fixes the **incorrect tracking** issue in the original solution and guarantees **the smallest valid subarray**. 🚀  

🚀 Edge Cases to Consider
1️⃣ All elements are the same
A = [5, 5, 5, 5]


- Expected Output: 1
- Explanation: The smallest subarray that contains both min and max is any single element since min == max.
2️⃣ Min and max occur at extreme ends
A = [3, 2, 4, 1]


- Min: 1, Max: 4
- Expected Output: 4
- Explanation: Only one valid subarray [3, 2, 4, 1] since min and max are far apart.
3️⃣ Multiple occurrences of min and max scattered
A = [2, 3, 2, 4, 3, 4, 2]


- Min: 2, Max: 4
- Expected Output: 2
- Explanation: [4, 2] (indices 5 and 6) is the smallest valid subarray.
4️⃣ Min and max occur at consecutive indices
A = [1, 4, 2, 3, 1, 4, 5]


- Min: 1, Max: 5
- Expected Output: 2
- Explanation: [1, 5] (indices 4 and 6) is the shortest subarray.
5️⃣ Edge Case: Only two elements
A = [3, 1]


- Expected Output: 2
- Explanation: Since both min and max exist in the entire array, the only possible subarray is the full array.
6️⃣ Edge Case: Min appears after max
A = [5, 2, 2, 5, 3, 2, 4, 5]


- Min: 2, Max: 5
- Expected Output: 2
- Explanation: [5, 2] (indices 3 and 4) is the shortest subarray.

# Attempts
1. Attempt 1
```
public class Solution {
    public int solve(int[] A) {
        int n = A.length;
        int min = Integer.MAX_VALUE;
        int max = Integer.MIN_VALUE;
        int minIndex = -1;
        int maxIndex = -1;
        int len = 0;

        for(int i=0;i<n;i++){
            min = Math.min(min, A[i]);
            max = Math.max(max, A[i]);
        }

        for(int i=0;i<n;i++){
            if(A[i]==min && maxIndex != -1){
                int newLen = i-maxIndex+1;
                if(newLen < len){
                    len = newLen;
                    minIndex = i;
                }
            }else if(A[i]==max && minIndex != -1){
                int newLen = i-minIndex+1;
                if(newLen < len){
                    len = newLen;
                    maxIndex = i;
                }
            }

            if(A[i] == min && minIndex == -1){
                minIndex = i;
            } else if(A[i] == max && maxIndex == -1){
                maxIndex = i;
            }
        }

        return len;
    }
}

```
✅ Issue 1 :   int len = 0 → Invalid Initial Value

You're trying to find the **minimum valid subarray length**, so initializing `len = 0` means no valid subarray will ever be smaller than it.

✅ Issue 2:  `minIndex` and `maxIndex` Are Not Updated Consistently

```java
if (A[i] == min && minIndex == -1) {
    minIndex = i;
}

```

❌ You're only setting `minIndex` and `maxIndex` **once**, the first time you encounter `min` or `max`.  
But to find the **shortest subarray**, you need to **update these indices every time** you see a new occurrence of `min` or `max`.

✅ **Fix:** Always update:

```java
if (A[i] == min) {
    minIndex = i;
    if (maxIndex != -1) {
        len = Math.min(len, i - maxIndex + 1);
    }
}
if (A[i] == max) {
    maxIndex = i;
    if (minIndex != -1) {
        len = Math.min(len, i - minIndex + 1);
    }
}

```

✅ Issue 3 :-  Incorrect Update Order

```java
if (A[i] == min && maxIndex != -1) {
    // update len
    minIndex = i;
}

```

You're updating `minIndex` **after** using it to compute `newLen`.  
This means you're using a **stale index** in the next iteration.

**Fix:** Update `minIndex` and `maxIndex` **before** using them to compute `len`.

[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
