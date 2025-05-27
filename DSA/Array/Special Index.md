#  Special Index

[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25455/assignment/problems/12828/hints?navref=cl_pb_nv_tb)
[Solution](#Solution)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)

**Problem Description**  

Given an array,  **arr[]**  of size  **N**, the task is to find the count of array indices such that removing an element from these indices makes the sum of even-indexed and odd-indexed array elements equal.

  
  
**Problem Constraints**  

1 <= N <= 105
-105 <= A[i] <= 105
Sum of all elements of A <= 109

  
  
**Input Format**  

First argument contains an array A of integers of size N

  
  
**Output Format**  

Return the count of array indices such that removing an element from these indices makes the sum of even-indexed and odd-indexed array elements equal.

  
  
**Example Input**  

Input 1:

A = [2, 1, 6, 4]

Input 2:

A = [1, 1, 1]

  
  
**Example Output**  

Output 1:

1

Output 2:

3

  
  
**Example Explanation**  

Explanation 1:

Removing arr[1] from the array modifies arr[] to { 2, 6, 4 } such that, arr[0] + arr[2] = arr[1]. 
Therefore, the required output is 1. 

Explanation 2:

Removing arr[0] from the given array modifies arr[] to { 1, 1 } such that arr[0] = arr[1] 
Removing arr[1] from the given array modifies arr[] to { 1, 1 } such that arr[0] = arr[1] 
Removing arr[2] from the given array modifies arr[] to { 1, 1 } such that arr[0] = arr[1] 
Therefore, the required output is 3.

[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
# Solution

Based on the observation that removing any element from the given array makes even indices of succeeding elements 
as odd and odd indices of the succeeding elements as even. 
Follow the steps below to solve the problem:

Initialize two variables, say evenSum and oddSum,
to store the sum of odd-indexed and even-indexed elements of the given array respectively.

Traverse the array using variable i.
Remove every ith element of the array and update the sum of the remaining even-indexed elements 
and the odd-indexed elements based on the above observation. Check if the sums are equal or not. 
If found to be true, then increment the count.

Finally, print the count obtained. Check out the complete solution for more clarity.


Time complexity : O(N) 
Space Complexity : O(1)

```java
public class Solution {

    // Function to count equilibrium indexes in the array
    private int cntIndexesToMakeBalance(int arr[], int n) {
        // If array has only one element, it's always an equilibrium index
        if (n == 1) {
            return 1;
        }

        // If the array has only two elements, no equilibrium index can exist
        if (n == 2)
            return 0;

        int sumEven = 0; // Stores sum of elements at even indices
        int sumOdd = 0;  // Stores sum of elements at odd indices

        // Calculate sum of even-indexed and odd-indexed elements
        for (int i = 0; i < n; i++) {
            if (i % 2 == 0) { // Even index
                sumEven += arr[i];
            } else { // Odd index
                sumOdd += arr[i];
            }
        }

        // Variables to track current sum while iterating
        int currOdd = 0; 
        int currEven = arr[0]; // First element is always at an even index
        int res = 0; // Stores the count of equilibrium indexes
        int newEvenSum = 0; // Stores recalculated even sum
        int newOddSum = 0; // Stores recalculated odd sum

        // Iterate through array to check for equilibrium indexes
        for (int i = 1; i < n - 1; i++) {
            if (i % 2 == 1) { // Odd index
                currOdd += arr[i];
                newEvenSum = currEven + sumOdd - currOdd; // Recalculate sum for even positions
                newOddSum = currOdd + sumEven - currEven - arr[i]; // Recalculate sum for odd positions
            } else { // Even index
                currEven += arr[i];
                newOddSum = currOdd + sumEven - currEven; // Recalculate sum for odd positions
                newEvenSum = currEven + sumOdd - currOdd - arr[i]; // Recalculate sum for even positions
            }

            // If recalculated sums are equal, it's an equilibrium index
            if (newEvenSum == newOddSum) {
                res++;
            }
        }

        // Special case: Check if the first or last element makes the array balanced
        if (sumOdd == sumEven - arr[0]) {
            res++;
        }
        if (n % 2 == 1) { // Odd-sized array
            if (sumOdd == sumEven - arr[n - 1]) {
                res++;
            }
        } else { // Even-sized array
            if (sumEven == sumOdd - arr[n - 1]) {
                res++;
            }
        }

        return res; // Return total count of equilibrium indexes
    }

    // Wrapper function that calls the main logic function
    public int solve(int[] A) {
        int n = A.length;
        return cntIndexesToMakeBalance(A, n);
    }
}
```

Clean code
```java
public class Solution {
    public int solve(int[] A) {
        int n = A.length;
        int oddSum = 0, evenSum = 0, ans = 0;

        // Step 1: Compute total odd and even index sums
        for (int i = 0; i < n; i++) {
            if (i % 2 == 0) {
                evenSum += A[i];
            } else {
                oddSum += A[i];
            }
        }

        int leftOdd = 0, leftEven = 0;

        // Step 2: Iterate through elements, checking if removing them balances sums
        for (int i = 0; i < n; i++) {
            // Remove current element from sum
            int remainingEven = evenSum - (i % 2 == 0 ? A[i] : 0);
            int remainingOdd = oddSum - (i % 2 != 0 ? A[i] : 0);

            // If removing the element keeps sums balanced, count it. See the explanation of the formula below.
            if (leftEven + remainingOdd == leftOdd + remainingEven) {
                ans++;
            }

            // Update left sums as if this element has been removed
            if (i % 2 == 0) {
                leftEven += A[i];
            } else {
                leftOdd += A[i];
            }
        }

        return ans;
    }
}
```


#### **🚀 Key Observation**

Yes, when we add `remainingOdd`, it includes `leftOdd`, and similarly, `leftEven` gets added along with `remainingEven`. But this **does not create double counting**—rather, it correctly **balances both sides**.

----------

#### **📌 Expanding the Formula**

We are checking:

```math
leftEven + remainingOdd == leftOdd + remainingEven

```

Breaking down each term:

-   **leftEven:** Sum of even-indexed elements **before** index `i`
-   **remainingOdd:** Sum of odd-indexed elements **after** index `i` (excluding `A[i]` if `i` is odd)
-   **leftOdd:** Sum of odd-indexed elements **before** index `i`
-   **remainingEven:** Sum of even-indexed elements **after** index `i` (excluding `A[i]` if `i` is even)

Now, let's rewrite `remainingEven` and `remainingOdd`:

```math
remainingEven = evenSum - leftEven - A[i] (if i is even)
remainingOdd  = oddSum - leftOdd - A[i] (if i is odd)

```

Substituting these into the equation:

```math
leftEven + (oddSum - leftOdd - A[i]) == leftOdd + (evenSum - leftEven - A[i])

```

Which simplifies to:

```math
leftEven + oddSum - leftOdd - A[i] == leftOdd + evenSum - leftEven - A[i]

```

Cancel `A[i]` on both sides:

```math
leftEven + oddSum - leftOdd == leftOdd + evenSum - leftEven

```

Rearrange:

```math
leftEven + oddSum == leftOdd + evenSum

```

Since `evenSum` and `oddSum` are constant totals, **this ensures both sides are equal**, meaning removing `A[i]` balances the sums!

----------

#### **🔥 Why This Works**

✔ **Each side correctly accounts for all elements** before and after removal.  
✔ **There is no double counting**—the equation correctly adjusts for shifts in indexing.  
✔ **Balanced sums mean valid index removal**, which is exactly what we want to find!

[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
