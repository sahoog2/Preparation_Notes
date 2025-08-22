
#  Max Sum Contiguous Subarray

[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25460/assignment/problems/56/hints?navref=cl_pb_nv_tb)
[Solution](#Solution)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
[Attempts](#Attempt)



**Problem Description**  

Given an array A of length N, your task is to find the  **maximum possible sum**  of any  **non-empty contiguous subarray**.  
  
In other words, among all possible subarrays of  **A**, determine the one that yields the  **highest sum**  and return that sum.

  
  
**Problem Constraints**  

1 <= N <= 106  
-1000 <= A[i] <= 1000

  
  
**Input Format**  

The first and the only argument contains an integer array, A.

  
  
**Output Format**  

Return an integer representing the maximum possible sum of the contiguous subarray.

  
  
**Example Input**  

Input 1:

 A = [1, 2, 3, 4, -10] 

Input 2:

 A = [-2, 1, -3, 4, -1, 2, 1, -5, 4] 

  
  
**Example Output**  

Output 1:

 10 

Output 2:

 6 

  
  
**Example Explanation**  

Explanation 1:

 The subarray [1, 2, 3, 4] has the maximum possible sum of 10. 

Explanation 2:

 The subarray [4,-1,2,1] has the maximum possible sum of 6.


[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25460/assignment/problems/56/hints?navref=cl_pb_nv_tb)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)

# Solution

Let us say  **Ai, Ai+1 … Aj**  is our optimal solution.

_Note that no prefix of the solution will ever have a negative sum._

Let us say Ai … Ak prefix had a negative sum.

Sum ( Ai Ai+1 … Aj ) = Sum (Ai … Ak) + Sum(Ak+1 … Aj)

Sum ( Ai Ai+1 … Aj) - Sum(Ak+1 … Aj) = Sum(Ai … Ak)

Now, since Sum(Ai … Ak) < 0,

Sum (Ai Ai+1 … Aj) - Sum (Ak+1 … Aj) < 0

which means Sum(Ak+1 … Aj ) > Sum (Ai Ai+1 … Aj)

This contradicts the fact that Ai, Ai+1 … Aj is our optimal solution.

Instead, Ak+1, Ak+2 … Aj will be our optimal solution.

Similarly, you can prove that it is always good to include a prefix with a positive sum for the optimal solution.

Try to come up with a solution based on the previous 2 facts.

Here’s one Approach.  
Keep two variables ‘curSum’ and ‘maxSum’ which denotes the current sum ending at the given position and the maximum sum of a subarray respectively.  
Iterate through the array , at every index we will add the current element to our curSum , after this we can update the maxSum as max(maxSum,curSum), After this we can just check if curSum is less than 0 , if it is then just replace curSum with 0.

**Time Complexity : O(n)**  
**Space Complexity(extra) : O(1)**

```java
public class Solution {
    // DO NOT MODIFY THE LIST. IT IS READ ONLY
    public int maxSubArray(final List<Integer> A) {
        int curSum = 0; //is the maximum sum ending at any given index i
        int maxSum = Integer.MIN_VALUE; // maximum subarray sum for all subarrays till now
	    for (int num : A) {
	        curSum += num;
            maxSum = Math.max(maxSum, curSum);
            if (curSum < 0) curSum = 0;
	    }
	    return maxSum;
    }
}
```
# Attempt
1. Attempt 1
```
public class Solution {
    public int maxSubArray(final int[] A) {
        int n = A.length;
        int sum = 0;
        int maxSum = Integer.MIN_VALUE;

        for(int i=0;i<n;i++){
            sum += A[i];
            if(sum <0){sum = 0;}
            maxSum = Math.max(sum,maxSum);
        }

        return maxSum;
    }
}

```
Issue 1:-

This solution will fail for a edge case like input - [-500].

The reason is order of below two lines. To get correct solution these two lines order need to be changed.

if(sum <0){sum = 0;}
maxSum = Math.max(sum,maxSum);


[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
