# Alternating Subarrays Easy

[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25460/homework/problems/16123/hints?navref=cl_pb_nv_tb)
[Solution](#Solution)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)


**Problem Description**  

You are given an integer array  **A**  of length  **N**  comprising of  **0's**  &  **1's**, and an integer  **B**.

You have to tell all the indices of array  **A**  that can act as a center of  **2 * B + 1**  length 0-1 alternating subarray.

A  **0-1 alternating array**  is an array containing only  **0's**  &  **1's**, and having no adjacent  **0's**  or  **1's**. For e.g. arrays  **[0, 1, 0, 1], [1, 0]**  and  **[1]**  are 0-1 alternating, while  **[1, 1]**  and  **[0, 1, 0, 0, 1]**  are not.

  
  
**Problem Constraints**  

**1**  <=  **N**  <=  **103**

**A[i]**  equals to  **0 or 1**.

**0**  <=  **B**  <=  **(N - 1) / 2**

  
  
**Input Format**  

First argument is an integer array  **A**.

Second argument is an integer  **B**.

  
  
**Output Format**  

Return an integer array containing indices(0-based) in  **sorted order**. If no such index exists, return an  **empty**  integer array.

  
  
**Example Input**  

Input 1:

 A = [1, 0, 1, 0, 1]
 B = 1 

Input 2:

 A = [0, 0, 0, 1, 1, 0, 1]
 B = 0 

  
  
**Example Output**  

Output 1:

 [1, 2, 3]

Output 2:

 [0, 1, 2, 3, 4, 5, 6]

  
  
**Example Explanation**  

Explanation 1:

 Index 1 acts as a centre of alternating sequence: **[A0, A1, A2]**
 Index 2 acts as a centre of alternating sequence: **[A1, A2, A3]**
 Index 3 acts as a centre of alternating sequence: **[A2, A3, A4]** 

Explanation 2:

 Each index in the array acts as the center of alternating sequences of lengths 1.

[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25460/homework/problems/16123/hints?navref=cl_pb_nv_tb)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
# Solution
Since, the length of the given required subarray is fixed, and the constraints allow an O(N ^ 2) approach.

We can simply brute force for each subarray for length 2 * B + 1.
We will loop from each starting point of every possible subarray, and check if the adjacent elements are unequal.

We can keep a flag variable to keep track of the status throughout the subarray.
If the condition is true, then we will append to a list that we will return.

Refer to the complete solution for more implementation details.

📌 Optimized Approach
✅ Iterate through all possible centers (i), checking if a subarray of length 2 * B + 1 exists around that index.
✅ Verify the 0-1 alternating pattern by checking adjacent elements.
✅ Use a sliding window technique to efficiently validate subarrays

Check after below code for solution

```java
import java.util.*;

public class Solution {
    public int[] solve(int[] A, int B) {
        ArrayList<Integer> ans = new ArrayList<>(); // Stores valid center indices
        int len = 2 * B + 1; // Required length of alternating subarray
        int n = A.length; // Length of input array

        // Iterate through all possible starting positions of the subarray
        for (int i = 0; i < n - len + 1; i++) {
            int prev = -1; // Variable to store previous element
            int flag = 1; // Flag to check if the subarray is alternating
            
            // Check if subarray from index i to i+len is alternating
            for (int j = i; j < i + len; j++) {
                if (A[j] == prev) { // If two adjacent elements are the same, it's not alternating
                    flag = 0; // Set flag to false
                    break; // Exit loop early
                }
                prev = A[j]; // Update previous element
            }
            
            // If valid, add the center index (i + B) to the result list
            if (flag == 1) {
                ans.add(i + B);
            }
        }

        // Convert ArrayList to an integer array for the final result
        int[] an = new int[ans.size()];
        for (int i = 0; i < ans.size(); i++) {
            an[i] = ans.get(i);
        }

        return an; // Return the list of valid center indices
    }

    public static void main(String[] args) {
        int[] A = {1, 0, 1, 0, 1, 1}; // Sample input
        int B = 2; // Length factor

        Solution sol = new Solution();
        int[] centers = sol.solve(A, B);

        System.out.println("Valid Centers: " + Arrays.toString(centers)); // Output expected: [2]
    }
}
```
```java
import java.util.ArrayList;
import java.util.List;

public class Solution {
    public List<Integer> findAlternatingCenters(int[] A, int B) {
        int n = A.length;
        int subArraySize = 2 * B + 1;
        List<Integer> centers = new ArrayList<>();

        for (int i = B; i < n - B; i++) { // Valid center range
            boolean isValid = true;

            // Check alternating pattern in subarray around index 'i'
            for (int j = i - B; j < i + B; j++) {
                if (A[j] == A[j + 1]) { // Two adjacent elements are the same
                    isValid = false;
                    break;
                }
            }

            if (isValid) {
                centers.add(i); // Index 'i' is a valid center
            }
        }

        return centers;
    }

    public static void main(String[] args) {
        int[] A = {0, 1, 0, 1, 0, 1, 0, 1, 0};
        int B = 2;

        Solution sol = new Solution();
        System.out.println("Valid Centers: " + sol.findAlternatingCenters(A, B));
        // Expected Output: [2, 3, 4, 5, 6] (Centers forming valid subarrays)
    }
}
```

[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
