# Counting Subarrays Easy

[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25460/homework/problems/16089/hints?navref=cl_pb_nv_tb)
[Solution](#Solution)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
[Attempt](#Attempt)


**Problem Description**  

Given an array  **A** of  **N**  non-negative numbers and a non-negative number **B,**  
you need to find the  **number of subarrays in A with a sum less than B.**  
We may assume that there is no overflow.

  
  
**Problem Constraints**  

1 <= N <= 5 x 103

1 <= A[i] <= 1000

1 <= B <= 107

  
  
**Input Format**  

First argument is an integer array  **A**.

Second argument is an integer  **B**.

  
  
**Output Format**  

Return an integer denoting the  **number of subarrays in A having sum less than B**.

  
  
**Example Input**  

Input 1:

 A = [2, 5, 6]
 B = 10

Input 2:

 A = [1, 11, 2, 3, 15]
 B = 10

  
  
**Example Output**  

Output 1:

 4

Output 2:

 4

  
  
**Example Explanation**  

Explanation 1:

 The subarrays with sum less than B are {2}, {5}, {6} and {2, 5},

Explanation 2:

 The subarrays with sum less than B are {1}, {2}, {3} and {2, 3}

[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25460/homework/problems/16089/hints?navref=cl_pb_nv_tb)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
# Solution
The constraints are small. Have you tried doing just what the question says?
Since the constraints are small we can generate all subarrays using 2 loops. This can be done in O(N^2). Then find the sum of each subarray and if the sum is less than B we add 1 to our answer.
Note that we cannot iterate over the subarray after generating the left index and right index to find the sum as this will increase the time complexity of the solution to O(N^3). We can find the sum of each subarray in O(1) with the help of a prefix sum array, which takes an O(N) precomputation.
Please refer to the complete solution for implementation.

📌 Optimized Approach (O(N))
✅ Use two pointers (left and right) to form a dynamic sliding window.
✅ Expand right → Add elements to the window.
✅ If sum exceeds or reaches B, move left to shrink the window.
✅ Every new subarray formed in the window contributes to the final count

See the solution after below code


```java
public class Solution {
    public int solve(int[] A, int B) {
        int n  = A.length;
        int pref[] = new int[n];
        pref[0]=A[0];
        int ans=0;
        for(int i=1;i<n;i++)pref[i]=pref[i-1]+A[i];
        for(int i=0;i<n;i++){
            for (int j=i;j<n;j++){
                int sum = pref[j];
                if(i>0){
                    sum -= pref[i-1];
                }
                if(sum < B) ans++;
            }
        }
        return ans;
    }
}
```

```java
public class Solution {
    public int countSubarrays(int[] A, int B) {
        int n = A.length;
        int count = 0, sum = 0;
        int left = 0;

        for (int right = 0; right < n; right++) {
            sum += A[right]; // Expand the window

            while (sum >= B && left <= right) {
                sum -= A[left]; // Shrink the window
                left++;
            }

            // Add subarrays ending at 'right'
            count += (right - left + 1);
        }

        return count;
    }

    public static void main(String[] args) {
        int[] A = {2, 5, 3, 10, 6};
        int B = 10;

        Solution sol = new Solution();
        System.out.println("Count of subarrays: " + sol.countSubarrays(A, B));  
        // Expected Output: 9
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
        int curr = 0;
        int ans = 0;

        for(int i=0;i<n;i++){
            sum += A[i];
            if(sum < B){
                ans++;
            }
            while(sum >= B && curr<n){
                sum -= A[curr];
                curr++;
            }
        }

        return ans;
    }
}

   ```

issue 1 : if(sum < B){
                ans++;
            }
lets assume for index 0 the sum is <B hence ans is updated to 1.
now for index 1 also sum (A[0] + A[1]) is < B hence ans is updated to 2
here the logic went wrong
no of sub arrays at index 0 = 1 {[0]},  ans is updated to 1
no of sub arrays at index 1 = 2 {[0,1],[1]} ans should be updated to ans = previous ans + new ans = 1+2 = 3. But the ans is updated to 2

so  if(sum < B){ ans++; } should be replaced with a logic which calculates the number of subarrays that can be formed with the current ending index i.e sum += (i-curr+1)

we can consider i as right and curr as left for better clarity. So the formula becomes sum += right - left +1
 
 2. Attempt 2

[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
