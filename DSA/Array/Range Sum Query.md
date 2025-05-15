#  Range Sum Query

[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25455/assignment/problems/15991/hints?navref=cl_pb_nv_tb)
[Solution](#Solution)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)


**Problem Description**  

You are given an integer array  **A**  of length  **N**.  
You are also given a 2D integer array  **B**  with dimensions  **M x 2**, where each row denotes a [L, R] query.  
For each query, you have to find the sum of all elements from L to R indices in A (0 - indexed).  
More formally, find A[L] + A[L + 1] + A[L + 2] +... + A[R - 1] + A[R] for each query.

  
  
**Problem Constraints**  

1 <= N, M <= 105  
1 <= A[i] <= 109  
0 <= L <= R < N

  
  
**Input Format**  

The first argument is the integer array A.  
The second argument is the 2D integer array B.

  
  
**Output Format**  

Return an integer array of length M where ith  element is the answer for ith  query in B.

  
  
**Example Input**  

Input 1:

```
A = [1, 2, 3, 4, 5]
B = [[0, 3], [1, 2]]

```

Input 2:

```
A = [2, 2, 2]
B = [[0, 0], [1, 2]]

```

  
  
**Example Output**  

Output 1:

```
[10, 5]

```

Output 2:

```
[2, 4]

```

  
  
**Example Explanation**  

Explanation 1:

The sum of all elements of A[0 ... 3] = 1 + 2 + 3 + 4 = 10.
The sum of all elements of A[1 ... 2] = 2 + 3 = 5.

Explanation 2:

```
The sum of all elements of A[0 ... 0] = 2 = 2.
The sum of all elements of A[1 ... 2] = 2 + 2 = 4.
```
[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25455/assignment/problems/15991/hints?navref=cl_pb_nv_tb)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
# Solution

We have to find a way to optimize the time complexity of answering our query.  
We can do this by creating an auxiliary array  **pref**,  
where pref[i] is the sum of all elements from the beginning to the ith  element.

We can easily create the pref array using the following equation:  
pref[i] = pref[i - 1] + A[i]

Now, we can answer all our queries in O(1).  
The answer to each query will be pref[R] - pref[L - 1].

**Time Complexity: O(N)**  
**Space Complexity: O(N)**

Refer to the complete solution for more details.

```java
public class Solution {
    public long[] rangeSum(int[] A, int[][] B) {
        int n = A.length;
        int m = B.length;
        long[] pref = new long[n + 1];
        pref[0] = A[0];
        for (int i = 1; i < n; i++) {
            pref[i] = pref[i - 1] + A[i];   // Sum from the 0th to the i-th index 
        }
        long[] ans = new long[m];
        for (int i = 0; i < m; i++) {
            ans[i] = pref[B[i][1]] - (B[i][0] > 0 ? pref[B[i][0] - 1] : 0);
        }
        return ans;
    }
}
```
[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25455/assignment/problems/15991/hints?navref=cl_pb_nv_tb)
[Solution](#Solution)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
