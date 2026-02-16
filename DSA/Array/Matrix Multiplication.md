
[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25462/assignment/problems/11464/hints?navref=cl_pb_nv_tb)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)

<details>
<summary>**Problem Description**</summary>
  You are given two integer matrices A(having M X N size) and B(having N X P). You have to multiply matrix A with B and return the resultant matrix. (i.e. return the matrix AB).

Matrix Multiplication 


Problem Constraints

1 <= M, N, P <= 100

-100 <= A[i][j], B[i][j] <= 100






Input Format

The first argument given is the 2-D integer matrix A.
The second argument given is the 2-D integer matrix B.



Output Format

Return a 2D integer matrix denoting AB.



Example Input

Input 1:

A = [[1, 2],
     [3, 4]]
B = [[5, 6],
     [7, 8]]
Input 2:

A = [[1, 1]]
B = [[2],
     [3]]





Example Output

Output 1:

 [[19, 22],
  [43, 50]]
Output 2:

 [[5]]


Example Explanation

Explanation 1:

 image
Explanation 2:

 [[1, 1]].[[2], [3]] = [[1 * 2 + 1 * 3]] = [[5]]
</details>

<details>
<summary>Approach</summary>
  If two matrices A (M x N) and B (N x P) are multiplied, then the order of the resultant matrix C will be (M x P).
Define a matrix C with size M x P with initial values equal to 0.
An individual (i, j)th element of resultant matrix is the sum of multiplications of elements of ith row of matrix A and all the elements of jth column of matrix B.
</details>   

<details>
<summary>Code</summary>
 </details> 
