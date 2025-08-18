#  Pick from both sides!

[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25455/assignment/problems/9900/hints?navref=cl_pb_nv_tb)
[Solution](#Solution)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
[Attempt](#Attempt)

**Problem Description**  

You are given an integer array  **A**  of size  **N**.

You have to perform  **B**  operations. In one operation, you can remove either the leftmost or the rightmost element of the array  **A**.

Find and return the  **maximum possible sum**  of the  **B elements**  that were removed after the  **B**  operations.

**NOTE:**  Suppose  **B = 3**, and array A contains 10 elements, then you can:

-   Remove 3 elements from front and 0 elements from the back, OR
-   Remove 2 elements from front and 1 element from the back, OR
-   Remove 1 element from front and 2 elements from the back, OR
-   Remove 0 elements from front and 3 elements from the back.

  
  
**Problem Constraints**  

1 <= N <= 105

1 <= B <= N

-103  <= A[i] <= 103

  
  
**Input Format**  

First argument is an integer array  **A**.

Second argument is an integer  **B**.

  
  
**Output Format**  

Return an integer denoting the maximum possible sum of elements you removed.

  
  
**Example Input**  

Input 1:

 A = [5, -2, 3 , 1, 2]
 B = 3

Input 2:

 A = [ 2, 3, -1, 4, 2, 1 ]
 B = 4

  
  
**Example Output**  

Output 1:

 8

Output 2:

 9

  
  
**Example Explanation**  

Explanation 1:

 Remove element 5 from front and element (1, 2) from back so we get 5 + 1 + 2 = 8

Explanation 2:

 Remove the first element and the last 3 elements. So we get 2 + 4 + 2 + 1 = 9
 
[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25455/assignment/problems/9900/hints?navref=cl_pb_nv_tb)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
# Solution

**Approach using Prefix and Suffix Sums:**

Maintain two arrays prefix[i] and suffix[i] where prefix[i] denotes sum of elements from index [0,i] and suffix[i] denotes sum of elements from index [i,N-1].

Now iterate from left and one by one pick elements from left for example: if you pick ‘a’ elements from left and remaining ‘k-a’ elements from right.  
So the sum in this case will be prefix[a-1] + suffix[n-(k-a)]

Maintain the maximum among all and return it.

**Time Complexity: O(N)**  
**Space Complexity: O(N)**

where N is number of elements in array A

Bonus: Try solving it in O(1) space.

```java
Method 0:
public class Solution {
    public int solve(int[] A, int B) {
        int n = A.length;
        int[] pa = new int[n];
        int[] sa = new int[n+1];
        int sum = 0;

        pa[0] = A[0];
        sa[n] = 0;

        for(int i=1;i<n;i++){
            pa[i] = pa[i-1]+A[i];
        }

        for(int i=n-1;i>=0;i--){
            sa[i] = sa[i+1]+A[i];
        }

        if(B==0){
            return sum;
        }

        sum = pa[B-1];
        if(sa[n-B]>sum){
            sum = sa[n-B];
        }

        //int tmp_sum = Integer.MIN_VALUE;

        for(int i=1;i<B;i++){
            //sum = Math.max(sum, pa[i-1] + sa[n-B+i]);
            int tmp_sum = pa[i-1] + sa[n-B+i];
            if(tmp_sum>sum){
                sum=tmp_sum;
                
            }

            tmp_sum=Integer.MIN_VALUE;
            
        }

        return sum;

        
    }
}


Method 1:

public class Solution {
    public int solve(int[] A, int B) {
        int n = A.length;
        int []suff = new int[n + 1];
        suff[n] = 0;
        suff[n - 1] = A[n - 1];
        for(int i = n - 2; i >= 0; i--){
            suff[i] = A[i] + suff[i + 1];
        }
        int pref_sum = 0;
        int ans = suff[n - B];
        for(int i = 0; i < B; i++){
            pref_sum = pref_sum + A[i];
            int suff_sum = suff[n - B + (i + 1)];
            ans = Math.max(ans, pref_sum + suff_sum);
        }
        return ans;
    }
}

Method 2:

public class Solution {
    public int solve(int[] A, int B) {
        int n = A.length;
        int cur = 0;
        for(int i = 0; i < B; i++){
            cur += A[i];
        }
        int back = B - 1; 
        int ans = cur; 
        for(int j = n - 1 ; j >= n-B; j--){
            cur += A[j];
            cur -= A[back];
            back--;
            ans = Math.max(ans, cur);
        }
        return ans;
    }
}
```

# Attempt
1. Attempt 1
   ```
   public class Solution {
    public int solve(int[] A, int B) {
        int n = A.length;
        int sum = 0;
        int maxSum = 0;
        for(int i=0; i<B; i++){
            sum += A[i];
        }

        maxSum = Math.max(maxSum,sum);
        int front = B-1;

        for(int i=n-1; i>=n-B-1; i--){
            sum = sum + A[i] - A[front];
            maxSum = Math.max(maxSum, sum);
            front--;
        }

        return maxSum;
    }
}

issue 1 : line no [maxSum = Math.max(maxSum,sum);]
          Here -ve number is not considered. If sum of B elements is -ve then maxSum is updated as 0 wrongly.
issue 2 : line no  [for(int i=n-1; i>=n-B+1; i--){]   (n = length of array, if n is 5 then the last index is 4) 
          for example if n = 6, B = 3. for 3 elements from back, i should traverse till 5,4 & 3 index.
          now with the formula 6-3+1 = 4, i will traverse till index 4 which is wrong.

   ```
