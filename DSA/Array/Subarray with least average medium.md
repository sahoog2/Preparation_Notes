# Subarray with least average

[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25460/assignment/problems/12827/hints?navref=cl_pb_nv_tb)
[Solution](#Solution)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
[Attempts](#Attempts)





**Problem Description**  

Given an array  **A**  of size  **N**, find the subarray of size  **B**  with the least average.

  
  
**Problem Constraints**  

1 <= B <= N <= 105
-105 <= A[i] <= 105 

  
  
**Input Format**  

First argument contains an array A of integers of size N.  
Second argument contains integer B.

  
  
**Output Format**  

Return the index of the first element of the subarray of size B that has least average.  
Array indexing starts from 0.

  
  
**Example Input**  

Input 1:

A = [3, 7, 90, 20, 10, 50, 40]
B = 3

Input 2:

A = [3, 7, 5, 20, -10, 0, 12]
B = 2

  
  
**Example Output**  

Output 1:

3

Output 2:

4

  
  
**Example Explanation**  

Explanation 1:

Subarray between indexes 3 and 5
The subarray {20, 10, 50} has the least average 
among all subarrays of size 3.

Explanation 2:

 Subarray between [4, 5] has minimum average




[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25460/assignment/problems/12827/hints?navref=cl_pb_nv_tb)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
# Solution
An Efficient Solution is to solve the above problem in O(N) time and O(1) extra space. The idea is to use sliding window of size B. Keep track of sum of current B elements. To compute sum of current window, remove first element of previous window and add current element (last element of current window).

1) Initialize res_index = 0 // Beginning of result index
2) Find sum of first B elements. Let this sum be 'curr_sum'
3) Initialize min_sum = sum
4) Iterate from (B+1)'th to n'th element, do following
   for every element arr[i]
      a) curr_sum = curr_sum + arr[i] - arr[i-B]
      b) If curr_sum < min_sum
           res_index = (i-B+1)
5) Return res_index as beginning index of resultant subarray.
```java
public class Solution {
    public int solve(int[] A, int B) {
        int n = A.length; // Get the size of the array
        int sum = 0; // Store the sum of the current subarray
        int ans = 0; // Store the starting index of the subarray with the least average

        // Compute the sum of the first subarray of size B
        for (int i = 0; i < B; i++) {
            sum += A[i];
        }

        int lSum = sum; // Track the minimum sum encountered so far

        // Slide the window across the array to check all subarrays of size B
        for (int i = 1; i <= (n - B); i++) {
            // Update the sum for the new window by subtracting the outgoing element
            // and adding the incoming element
            sum = sum + A[B + i - 1] - A[i - 1];

            // If the new sum is smaller, update lSum and store the new starting index
            if (sum < lSum) {
                lSum = sum;
                ans = i;
            }
        }

        // Return the starting index of the subarray with the least average
        return ans;
    }
}
```

# Attempts

1. Attempt 1
```
public class Solution {
    public int solve(int[] A, int B) {
        int n = A.length;
        int sum = 0;
        for(int i=0;i<B;i++){
            sum += A[i];
        }

        int lstAvg = sum/B;
        int ans = 0;

        for(int j=0;j<n-B;j++){
            sum = sum - A[j] + A[j+B];
            int avg = sum/B;
            if(avg < lstAvg){
                ans = j;
                lstAvg = avg;
            }
        }

        return ans;
    }
}

```

Issue 1:
This solution will fail for below input :-

A = [18,11,16,19,11,9,8,15,3,10,9,20,1,19]

B = 1;

The reason is:

Before the for loop the B size array average is already calculated and the index is stored in variable ans.

In the for loop as part of sliding window technology, for j=0, the 0 index is subtracted and B^th^ index is added. This means the subarray from index 1 is being calculated.

However in the if clause we are saving j as answer. This should have been j+1. 

[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
