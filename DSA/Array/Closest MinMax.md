#  Closest MinMax

[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25458/assignment/problems/986/hints?navref=cl_pb_nv_tb)
[Solution](#Solution)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)


**Problem Description**  

Given an array  **A**, find the size of the smallest subarray such that it contains at least one occurrence of the maximum value of the array

and at least one occurrence of the minimum value of the array.

  
  
**Problem Constraints**  

1 <=  **|A|**  <= 2000

  
  
**Input Format**  

First and only argument is vector  **A**

  
  
**Output Format**  

Return the length of the smallest subarray which has at least one occurrence of minimum and maximum element of the array

  
  
**Example Input**  

Input 1:

A = [1, 3, 2]

Input 2:

A = [2, 6, 1, 6, 9]

  
  
**Example Output**  

Output 1:

 2

Output 2:

 3

  
  
**Example Explanation**  

Explanation 1:

 Take the 1st and 2nd elements as they are the minimum and maximum elements respectievly.

Explanation 2:

 Take the last 3 elements of the array.

[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25458/assignment/problems/986/hints?navref=cl_pb_nv_tb)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)

# Solution

This problem can be solved in a simple O(N) complexity.  
We can implement a sliding window kind of algorithm using two pointers. We can slide over the array and keep track of every last occurrence of the minimum and maximum element of the array.  
In order to find the start point, we can simply remember the last occurrences of a minimum and a maximum value, respectively. And for each min-max pair, we check the length of the subarray that encloses them and then update out overall based on that.

**Time Complexity : O(n)**  
**Space Complexity(extra) : O(1)**

```
public class Solution {
    public int solve(int[] A) {
        
        int min_ele = Integer.MAX_VALUE, max_ele = Integer.MIN_VALUE;   // min and max value of the array
        int min_Index = -1, max_Index = -1; // index of the last element having value equal to min_ele and max_ele
        
        int ans = Integer.MAX_VALUE;
        for(int x:A){
            min_ele = Math.min(min_ele, x);
            max_ele = Math.max(max_ele, x);
        }
        
        for(int i=0 ; i<A.length ; i++){
            if(A[i] == min_ele) min_Index = Math.max(min_Index, i);
            if(A[i] == max_ele) max_Index = Math.max(max_Index, i);
            
            if(min_Index != -1 && max_Index != -1){
                int len = Math.abs(max_Index - min_Index) + 1;
                ans = Math.min(ans, len);
            }
        }
        
        return ans;
    }
}
```

[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
