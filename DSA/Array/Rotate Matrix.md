
[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25462/assignment/problems/55/hints?navref=cl_pb_nv_tb)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)

<details>
<summary>**Problem Description**</summary>
  You are given a n x n 2D matrix A representing an image.

Rotate the image by 90 degrees (clockwise).

You need to do this in place.

Note: If you end up using an additional array, you will only receive partial score.



Problem Constraints

1 <= n <= 1000



Input Format

First argument is a 2D matrix A of integers



Output Format

Return the 2D rotated matrix.



Example Input

Input 1:

 [
    [1, 2],
    [3, 4]
 ]
Input 2:

 [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
 ]


Example Output

Output 1:

 [
    [3, 1],
    [4, 2]
 ]
Output 2:

 [
    [7, 4, 1],
    [8, 5, 2],
    [9, 6, 3]
 ]


Example Explanation

Explanation 1:

 After rotating the matrix by 90 degree:
 1 goes to 2, 2 goes to 4
 4 goes to 3, 3 goes to 1
Explanation 2:

 After rotating the matrix by 90 degree:
 1 goes to 3, 3 goes to 9
 2 goes to 6, 6 goes to 8
 9 goes to 7, 7 goes to 1
 8 goes to 4, 4 goes to 2
</details>

<details>
<summary>Approach</summary>

  Take the transpose of the given matrix.
Reverse every row of the matrix to get the desired output.

Time Complexity: O(N^2)
Space Complexity: O(1)
</details>   

<details>
<summary>Code</summary>

  ```java
public  class Solution {

public  void solve(ArrayList<ArrayList<Integer>> A)  {

int n = A.size();

// ArrayList<ArrayList<Integer>> ans = new ArrayList<>();

// for(int i=0;i<n;i++){

// ArrayList<Integer> tmp = new ArrayList<>();

// for(int j=0;j<n;j++){

// tmp.add(0);

// }

// ans.add(tmp);

// }

  

for(int i=0;i<n;i++){

for(int j=i+1; j<n;j++){

int tmp = A.get(i).get(j);

A.get(i).set(j, A.get(j).get(i));

A.get(j).set(i, tmp);

}

}

  

for(int i=0;i<n;i++){

for(int j=0;j<n/2;j++){

int tmp = A.get(i).get(j);

A.get(i).set(j, A.get(i).get(n-j-1));

A.get(i).set(n-j-1, tmp);

}

}

}

}
```
 </details> 
