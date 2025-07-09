[Solution](#SOLUTION)  [Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25475/assignment/problems/167/hints?navref=cl_pb_nv_tb)  [Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Sorting/002%20problems.md)

Q1.  Sort by ColorSolved


**Problem Description**  

Given an array with  **N**  objects colored  **red, white, or blue**, sort them so that objects of the same color are adjacent, with the colors in the  **order red, white, and blue.  
  
**We will represent the colors as,

`red -> 0`  
`white -> 1`  
`blue -> 2`

**Note:**  Using the library sort function is not allowed.

  
  
**Problem Constraints**  

1 <= N <= 1000000  
0 <= A[i] <= 2

  
  
**Input Format**  

First and only argument of input contains an integer array A.

  
  
**Output Format**  

Return an integer array in asked order

  
  
**Example Input**  

Input 1 :

```
    A = [0, 1, 2, 0, 1, 2]

```

Input 2:

```
    A = [0]
```

  
  
**Example Output**  

Output 1:

```
    [0, 0, 1, 1, 2, 2]

```

Output 2:

```
    [0]
```

  
  
**Example Explanation**  

Explanation 1:

```
    [0, 0, 1, 1, 2, 2] is the required order.
```

Explanation 2:

```
    [0] is the required order
```

# SOLUTION
There are multiple approaches possible here. We need to make sure we do not allocate extra memory.

**Approach 1:**

> Count the number of red, white, and blue balls.  
> Then, in another pass, set the initial redCount number of cells as 0, next whiteCount cell as 1, and next blueCount cells as 2.  
> _Requires two passes of the array._

**Approach 2:**

> Swap the 0s to the start of the array maintaining a pointer, and 2s to the end of the array.  
> 1s will automatically be in their right position.

```java
public class Solution {
	public ArrayList<Integer> sortColors(ArrayList<Integer> A) {
	    
	    int zero = 0;
	    int two = A.size() - 1;
	    
	    for (int i = 0; i <= two;) {
	        if (A.get(i) == 0) {
	            int temp = A.get(zero);
	            A.set(zero, 0);
	            A.set(i, temp);
	            zero++;
	            i++;
	        } else if (A.get(i) == 2) {
	            int temp = A.get(two);
	            A.set(two, 2);
	            A.set(i, temp);
	            two--;
	        } else {
	            i++;
	        }
	    }
	    return A;
	}
}
```
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Sorting/002%20problems.md)
