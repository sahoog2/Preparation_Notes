#  Even Subarrays

[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25458/homework/problems/1176/hints?navref=cl_pb_nv_tb)
[Solution](#Solution)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)

**Problem Description**  

You are given an integer array  **A**.

Decide whether it is possible to divide the array into one or more subarrays of  **even length**  such that the  **first**  and  **last**  element of all subarrays will be  **even**.

Return "**YES**" if it is possible; otherwise, return "**NO**" (without quotes).

  
  
**Problem Constraints**  

1 <= |A|, A[i] <= 106

  
  
**Input Format**  

The first and the only input argument is an integer array, A.

  
  
**Output Format**  

Return a string "YES" or "NO" denoting the answer.

  
  
**Example Input**  

Input 1:

 A = [2, 4, 8, 6]

Input 2:

 A = [2, 4, 8, 7, 6]

  
  
**Example Output**  

Output 1:

 "YES"

Output 2:

 "NO"

  
  
**Example Explanation**  

Explanation 1:

 We can divide A into [2, 4] and [8, 6].

Explanation 2:

 There is no way to divide the array into even length subarrays.

[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25458/homework/problems/1176/hints?navref=cl_pb_nv_tb)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)

# Solution

If the first and the last element are even and the size of the array is even, then only the answer will be “YES.”  
Otherwise will be “NO,” as we can’t divide the array into subarrays that meet the given conditions in the question.

So, if(A[0]%2 == 0 and A[n-1]%2 == 0 and n%2 == 0)  
return “YES”;

```java
public class Solution {
    public String solve(int[] A) {
        int n = (int)A.length;
        if(A[0]%2 == 0 && A[n-1]%2 == 0 && n%2 == 0)
            return "YES";
        return "NO";
    }
}
```

[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
