[Solution](#SOLUTION) [Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25475/assignment/problems/372/hints?navref=cl_pb_nv_tb)  [Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Sorting/002%20problems.md)

Q4.  Noble Integer



**Problem Description**  

Given an integer array  **A**, find if an integer  **p**  exists in the array such that the number of integers greater than  **p**  in the array equals  **p**.

  
  
**Problem Constraints**  

1 <= |A| <= 2*105  
-108  <= A[i] <= 108

  
  
**Input Format**  

First and only argument is an integer array A.

  
  
**Output Format**  

Return 1 if any such integer p is present else, return -1.

  
  
**Example Input**  

Input 1:

 A = [3, 2, 1, 3]

Input 2:

 A = [1, 1, 3, 3]

  
  
**Example Output**  

Output 1:

 1

Output 2:

 -1

  
  
**Example Explanation**  

Explanation 1:

 For integer 2, there are 2 greater elements in the array..

Explanation 2:

 There exist no integer satisfying the required conditions.

# SOLUTION

First, we sort the input array.

Now, all we have to do is to traverse through each element of the array and check whether it matches our given statement. 
Since the array is sorted, we directly know how many elements are greater than that number in the array.

**Note: Please take care of cases when a certain element repeats many times.**

```
public class Solution {
    public int solve(ArrayList<Integer> A) {
        Collections.sort(A);
        int size = A.size();
        for(int i = 0; i < size; i++){
        	while(i+1<size && A.get(i)==A.get(i+1))
        		i++;
        	if(A.get(i) == size-1-i)
        		return 1;
        }
        return -1;
    }
}
```
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Sorting/002%20problems.md)
