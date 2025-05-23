#  Equilibrium index of an array
[Solution](#SOLUTION)
[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25455/assignment/problems/12826/hints?navref=cl_pb_nv_tb)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)

**Problem Description**  

You are given an array  **A** of integers of size  **N**.

Your task is to find the equilibrium index of the given array

The equilibrium index of an array is an index such that the sum of elements at lower indexes is equal to the sum of elements at higher indexes.

If there are no elements that are at lower indexes or at higher indexes, then the corresponding sum of elements is considered as 0.

**Note:**

-   Array indexing starts from 0.
-   If there is no equilibrium index then return -1.
-   If there are more than one equilibrium indexes then return the minimum index.

  
  
**Problem Constraints**  

1 <= N <= 105
-105 <= A[i] <= 105

  
  
**Input Format**  

First arugment is an array A .

  
  
**Output Format**  

Return the equilibrium index of the given array. If no such index is found then return -1.

  
  
**Example Input**  

Input 1:

A = [-7, 1, 5, 2, -4, 3, 0]

Input 2:

A = [1, 2, 3]

  
  
**Example Output**  

Output 1:

3

Output 2:

-1

  
  
**Example Explanation**  

Explanation 1:

i   Sum of elements at lower indexes    Sum of elements at higher indexes
0                   0                                   7
1                  -7                                   6
2                  -6                                   1
3                  -1                                  -1
4                   1                                   3
5                  -3                                   0
6                   0                                   0

3 is an equilibrium index, because: 
A[0] + A[1] + A[2] = A[4] + A[5] + A[6]

Explanation 1:

i   Sum of elements at lower indexes    Sum of elements at higher indexes
0                   0                                   5
1                   1                                   3
2                   3                                   0
Thus, there is no such index.
[Solution](#SOLUTION)
[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25455/assignment/problems/12826/hints?navref=cl_pb_nv_tb)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)

# Solution

The idea is to get the total sum of the array first. Then Iterate through the array and keep updating the left sum which is initialized as zero. In the loop, we can get the right sum by subtracting the elements one by one.

1) Initialize leftsum  as 0
2) Get the total sum of the array as sum
3) Iterate through the array and for each index i, do following.
    a)  Update sum to get the right sum.  
           sum = sum - arr[i] 
       // sum is now right sum
    b) If leftsum is equal to sum, then return current index. 
       // update leftsum for next iteration.
    c) leftsum = leftsum + arr[i]
4) return -1 
// If we come out of loop without returning then
// there is no equilibrium index

Time Complexity : O(N)
Space Complexity : O(1)

```java
    public class Solution {
    public int solve(int[] A) {
        long sum1 = 0;  // Stores the total sum of array elements
        
        // Calculate the total sum of the array elements
        for(int i = 0; i < A.length ; i++)  
            sum1 += A[i];

        long sum2 = 0;  // Tracks sum of elements before the current index
        int ans = Integer.MAX_VALUE; // Stores the equilibrium index (initialized to MAX_VALUE)

        // Iterate through the array to find the equilibrium index
        for(int i = 0 ; i < A.length ; i++) {
            sum1 -= A[i];   // Update sum1 to exclude the current element (sum of elements after index i)
            
            // Check if sum of elements on left (`sum2`) equals sum of elements on right (`sum1`)
            if(sum1 == sum2){
                ans = i;  // Found equilibrium index, store it
                break;    // No need to check further, exit loop
            }

            sum2 += A[i]; // Add current element to sum2 (sum of elements before index i)
        }

        // If no equilibrium index is found, return -1
        if(ans == Integer.MAX_VALUE)
            ans = -1;   

        return ans;
    }
}
```


[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
