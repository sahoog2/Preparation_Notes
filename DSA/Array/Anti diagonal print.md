<details>
<summary>**Problem Description**</summary>

Give a N * N square matrix A, return an array of its anti-diagonals. Look at the example for more details.  
  
   Problem Constraints  
 
   1<= N <= 1000  
   1<= A[i][j] <= 1e9  
 
 
   Input Format  
 
   Only argument is a 2D array A of size N * N.  
 
 
   Output Format  
 
   Return a 2D integer array of size (2 * N-1) * N, representing the anti-diagonals of input array A.  
   The vacant spaces in the grid should be assigned to 0.  
 
 
   Example Input  
 
   Input 1:  
   1 2 3  
   4 5 6  
   7 8 9  
   Input 2:  
 
   1 2  
   3 4  
 
 
   Example Output  
 
   Output 1:  
   1 0 0  
   2 4 0  
   3 5 7  
   6 8 0  
   9 0 0  
   Output 2:  
 
   1 0  
   2 3  
   4 0  
 
 
   Example Explanation  
 
   For input 1:  
   The first anti diagonal of the matrix is [1 ], the rest spaces shoud be filled with 0 making the row as [1, 0, 0].  
   The second anti diagonal of the matrix is [2, 4 ], the rest spaces shoud be filled with 0 making the row as [2, 4, 0].  
   The third anti diagonal of the matrix is [3, 5, 7 ], the rest spaces shoud be filled with 0 making the row as [3, 5, 7].  
   The fourth anti diagonal of the matrix is [6, 8 ], the rest spaces shoud be filled with 0 making the row as [6, 8, 0].  
   The fifth anti diagonal of the matrix is [9 ], the rest spaces shoud be filled with 0 making the row as [9, 0, 0].  
   For input 2:  
 
   The first anti diagonal of the matrix is [1 ], the rest spaces shoud be filled with 0 making the row as [1, 0, 0].  
   The second anti diagonal of the matrix is [2, 4 ], the rest spaces shoud be filled with 0 making the row as [2, 4, 0].  
   The third anti diagonal of the matrix is [3, 0, 0 ], the rest spaces shoud be filled with 0 making the row as [3, 0, 0].

</details>

<details>
<summary>Approach</summary>
  
Think of anti‑diagonal printing as **walking through the matrix by index sums**. The intuition is:

----------

### 1. Each anti‑diagonal is defined by `row + col`

-   In a 2D array, elements that lie on the same anti‑diagonal share the same sum of indices.
-   Example: `(0,2), (1,1), (2,0)` all have `row+col = 2`.

----------

### 2. Traverse by diagonals, not rows

-   Instead of scanning row by row, you group elements by their index sum.
-   Start with sum = 0 (top‑left corner), then sum = 1, sum = 2, … until sum = `n+m-2`.

----------

### 3. Collect elements for each sum

-   For a given sum `s`, valid positions are `(i, j)` where:
    -   `i + j = s`
    -   `i` is within row bounds
    -   `j` is within column bounds
-   This gives you the elements of that anti‑diagonal.

----------

### 4. Print diagonals in order

-   Begin with the top row, moving right.
-   Then continue from the last column, moving down.
-   Each time, collect elements along the anti‑diagonal and print them.

----------

### 📚 Example

Matrix:

```
1 2 3
4 5 6
7 8 9

```

-   Sum = 0 → `(0,0)` → `1`
-   Sum = 1 → `(0,1),(1,0)` → `2,4`
-   Sum = 2 → `(0,2),(1,1),(2,0)` → `3,5,7`
-   Sum = 3 → `(1,2),(2,1)` → `6,8`
-   Sum = 4 → `(2,2)` → `9`

Output:

```
1
2 4
3 5 7
6 8
9

```

----------

### ✅ Key Insight

The trick is to realize that **anti‑diagonals are indexed by the sum of row and column indices**. Once you see that, printing them is just looping over possible sums and collecting elements.

</details>   

<details>
<summary>Code</summary>
  
Here’s a clear Java implementation that follows the intuition we discussed — grouping elements by the sum of their indices (`row + col`) to print anti‑diagonals:

```java
public class AntiDiagonal {
    public static void printAntiDiagonals(int[][] matrix) {
        int n = matrix.length;        // number of rows
        int m = matrix[0].length;     // number of columns

        // The maximum sum of indices is (n-1 + m-1)
        for (int sum = 0; sum <= n + m - 2; sum++) {
            // For each possible sum, collect elements
            for (int i = 0; i < n; i++) {
                int j = sum - i; // column index
                if (j >= 0 && j < m) {
                    System.out.print(matrix[i][j] + " ");
                }
            }
            System.out.println(); // move to next anti-diagonal
        }
    }

    public static void main(String[] args) {
        int[][] matrix = {
            {1, 2, 3},
            {4, 5, 6},
            {7, 8, 9}
        };

        printAntiDiagonals(matrix);
    }
}

```

----------

### 🧠 How It Works

-   Outer loop: iterates over all possible sums of indices (`sum = 0` to `n+m-2`).
-   Inner loop: for each row `i`, compute column `j = sum - i`.
-   If `j` is valid, print `matrix[i][j]`.
-   This groups elements by anti‑diagonal.

----------

### 📚 Example Output for 3×3 Matrix

```
1
2 4
3 5 7
6 8
9

```

----------

This approach is efficient (`O(n*m)`) and works for any rectangular matrix, not just square ones.

</details> 
