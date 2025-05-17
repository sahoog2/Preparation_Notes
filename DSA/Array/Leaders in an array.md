#  Leaders in an array

[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25458/homework/problems/11921/hints?navref=cl_pb_nv_tb)
[Solution](#Solution)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)


**Problem Description**  

Given an integer array  **A**  containing  **N**  distinct integers, you have to find  **all the leaders**  in array  **A**. An element is a leader if it is  **strictly greater than**  all the elements to its  **right side.**  
  
**NOTE**: The rightmost element is always a leader.

  
  
**Problem Constraints**  

1 <= N <= 105  
1 <= A[i] <= 108

  
  
**Input Format**  

There is a single input argument which a integer array  **A**

  
  
**Output Format**  

Return an integer array denoting all the  **leader elements**  of the array.

  
  
**Example Input**  

Input 1:

 A = [16, 17, 4, 3, 5, 2]

Input 2:

 A = [5, 4]

  
  
**Example Output**  

Output 1:

[17, 2, 5]

Output 2:

[5, 4]

  
  
**Example Explanation**  

Explanation 1:

 Element 17 is strictly greater than all the elements on the right side to it.  
 Element 2 is strictly greater than all the elements on the right side to it.  
 Element 5 is strictly greater than all the elements on the right side to it.  
 So we will return these three elements i.e [17, 2, 5], we can also return [2, 5, 17] or [5, 2, 17] or any other ordering.

Explanation 2:

 Element 5 is strictly greater than all the elements on the right side to it.  
 Element 4 is strictly greater than all the elements on the right side to it.  
 So we will return these two elements i.e [5, 4], we can also any other ordering.

[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25458/homework/problems/11921/hints?navref=cl_pb_nv_tb)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)

# Solution
**Method 1: (Simple)**

Use two loops. The outer loop runs from 0 to size – 1 and, one by one, picks all elements from left to the right. The inner loop compares the picked element to all the elements to its right side. If the picked element is greater than all the elements to its right side, then the picked element is the leader.  
Time Complexity: O(N2)

**Method 2: (Scan from right) Optimized Approach**

Note that for an element to be greater than all the elements towards its right , it just needs to be greater than the maximum element towards its right.  
Keep a variable ‘mx’ which stores the maximum till now and initialize it with the last element of the array and also add the last element to our answer array. Iterate from n-2 to 0 , at every index we check if that number is greater than the variable mx. If it is we add the element to our answer array and change mx to that variable.

Time Complexity: O(N)  
Space Complexity: O(1)

```java
public class Solution {
    public int[] solve(int[] A) {
        int size = A.length;

        int[] ans = new int[size];
        int max_from_right = A[size - 1];
        int count = 0;
        ans[count++] = max_from_right;

        for (int i = size - 2; i >= 0; i--) {
            if (max_from_right < A[i]) {
                ans[count++] = A[i];
                max_from_right = A[i];
            }
        }

        int[] result = new int[count];
        for (int i = 0; i < count; i++) {
            result[i] = ans[i];
        }
        return result;
    }
}
```


[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
