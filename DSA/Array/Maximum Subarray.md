# Maximum Subarray Easy

[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25460/assignment/problems/16121/hints?navref=cl_pb_nv_tb)
[Solution](#Solution)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)


**Problem Description**  

You are given an integer array  **C**  of size  **A**. Now you need to find a subarray (contiguous elements) so that the sum of contiguous elements is maximum.  
But the sum must not exceed  **B**.

  
  
**Problem Constraints**  

1 <= A <= 103  
1 <= B <= 109  
1 <= C[i] <= 106  

  
  
**Input Format**  

The first argument is the integer A.  
The second argument is the integer B.  
The third argument is the integer array C.

  
  
**Output Format**  

Return a single integer which denotes the maximum sum.

  
  
**Example Input**  

Input 1:

```
A = 5
B = 12
C = [2, 1, 3, 4, 5]

```

Input 2:

```
A = 3
B = 1
C = [2, 2, 2]

```

  
  
**Example Output**  

Output 1:

```
12

```

Output 2:

```
0

```

  
  
**Example Explanation**  

Explanation 1:

We can select {3,4,5} which sums up to 12 which is the maximum possible sum.

Explanation 2:

All elements are greater than B, which means we cannot select any subarray.
Hence, the answer is 0.

[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25460/assignment/problems/16121/hints?navref=cl_pb_nv_tb)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
# Solution
####  Brute Force Solution Explanation

The brute-force approach involves **checking all possible subarrays** and finding the one with the **maximum sum** while ensuring the sum **does not exceed B**

#####  Approach

1️⃣ Iterate through all **possible starting indices** in the array.  
2️⃣ Iterate through all **possible ending indices** for each start index to form subarrays.  
3️⃣ Calculate the sum for each subarray and **track the maximum valid sum** (≤ B).

Since we check **all possible subarrays**, this approach has a **time complexity of O(N²)**.

----------

##### Brute Force Java Implementation

```java
public class Solution {
    public int maxSubarraySum(int[] C, int B) {
        int n = C.length;
        int maxSum = 0;

        // Try all possible subarrays
        for (int i = 0; i < n; i++) {
            int sum = 0;
            
            for (int j = i; j < n; j++) {
                sum += C[j]; // Extend subarray to include C[j]

                if (sum <= B) { // Ensure sum does not exceed B
                    maxSum = Math.max(maxSum, sum);
                } else {
                    break; // Stop further additions if sum exceeds B
                }
            }
        }
        
        return maxSum;
    }

    public static void main(String[] args) {
        int[] C = {3, 2, 5, 8, 1}; // Sample input
        int B = 10; // Maximum allowed sum

        Solution sol = new Solution();
        System.out.println("Max Subarray Sum: " + sol.maxSubarraySum(C, B)); 
        // Expected Output: 10 (e.g., subarray [3,2,5] or [8,1])
    }
}

```

----------

##### **🚀 Complexity Analysis**

✅ **O(N²) Time Complexity** → Iterating over all possible subarrays.  
✅ **O(1) Space Complexity** → Uses only a few variables.

####  Optimized Solution Using Sliding Window (O(N) Complexity)

Instead of checking **all subarrays**, we can use a **Sliding Window** approach to efficiently find the maximum sum without exceeding B

##### Approach

✅ Maintain a **window with a valid sum** (≤ B).  
✅ **Expand right** to include elements.  
✅ If sum **exceeds B**, **shrink the left** side until it's valid again.  
✅ Track the maximum valid sum encountered.


##### Java Implementation

```java
public class Solution {
    public int maxSubarraySum(int[] C, int B) {
        int n = C.length;
        int maxSum = 0;
        int sum = 0;
        int left = 0; // Left boundary of sliding window

        // Expand right boundary
        for (int right = 0; right < n; right++) {
            sum += C[right]; // Add new element to sum
            
            // Shrink left boundary while sum exceeds B
            while (sum > B && left <= right) {
                sum -= C[left]; // Remove leftmost element
                left++; // Move left boundary forward
            }

            // Update maxSum if the sum is valid
            maxSum = Math.max(maxSum, sum);
        }
        
        return maxSum;
    }

    public static void main(String[] args) {
        int[] C = {3, 2, 5, 8, 1}; // Sample input
        int B = 10; // Maximum allowed sum

        Solution sol = new Solution();
        System.out.println("Max Subarray Sum: " + sol.maxSubarraySum(C, B)); 
        // Expected Output: 10 (e.g., subarray [3,2,5] or [8,1])
    }
}

```

----------

##### Why Is This Optimized?

✅ **O(N) Complexity:** Each element is processed **at most twice**.  
✅ **No unnecessary re-computation:** Avoids recalculating sum for all subarrays.  
✅ **Efficient for large inputs:** Suitable for **competitive programming** scenarios.

[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
