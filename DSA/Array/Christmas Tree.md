

[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25464/assignment/problems/1083/hints?navref=cl_pb_nv_tb)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)

<details>
<summary>**Problem Description**</summary>

You are given an array  **A**  consisting of heights of Christmas trees and an array  **B**  of the same size consisting of the cost of each of the trees (**Bi**  is the cost of tree  **Ai**, where  **1 ≤ i ≤ size(A**)), and you are supposed to choose  **3**  trees (let's say, indices p, q, and r), such that  **Ap  < Aq  < Ar**, where  **p < q < r**.  
The cost of these trees is  **Bp  + Bq  + Br**.

You are to choose  **3**  trees such that their total cost is minimum. Return that cost.

If it is not possible to choose 3 such trees return  **-1**.

  
  
**Problem Constraints**  

1 <= A[i], B[i] <= 109  
3 <= size(A) = size(B) <= 3000

  
  
**Input Format**  

First argument is an integer array A.  
Second argument is an integer array B.

  
  
**Output Format**  

Return an integer denoting the minimum cost of choosing 3 trees whose heights are strictly in increasing order, if not possible, -1.

  
  
**Example Input**  

Input 1:

 A = [1, 3, 5]
 B = [1, 2, 3]

Input 2:

 A = [1, 6, 4, 2, 6, 9]
 B = [2, 5, 7, 3, 2, 7]

  
  
**Example Output**  

Output 1:

 6 

Output 2:

 7 

  
  
**Example Explanation**  

Explanation 1:

 We can choose the trees with indices 1, 2 and 3, and the cost is 1 + 2 + 3 = 6. 

Explanation 2:

 We can choose the trees with indices 1, 4 and 5, and the cost is 2 + 3 + 2 = 7. 
 This is the minimum cost that we can get.
</details>

<details>
<summary>Approach</summary>

To solve this, let’s take three indices,  _p_,  _q_  and  _r_.

-   _p_  is the index of the tree that is to be chosen first, i.e. the one with the smallest height.
-   _q_  is the index of the tree that is to be chosen second, i.e. the one with the middle height.
-   _r_  is the index of the tree that is to be chosen third, i.e. the one with the largest height.

We should now traverse the array by fixing index  _q_. Lets  **N**  be the size of the array.

For  _q_, that goes from index q+1 to  **N**-1, we can find an index  _p_  that goes from 1 to  _q_-1 such that  **A**[_p_] <  **A**[_q_], and  **B**[_p_] is minimum.  
Similarly, find an index  _r_  that goes from  _q_+1 to  **N**  such that  **A**[_r_] >  **A**[_q_], and  **B**[_r_] is minimum.

This way, for all  _q_  we can find the minimum values, and we choose the minimum values from all the  _q_  values.

**Time Complexity : O(n^2)**  
**Space Complexity(extra) : O(1)**
</details>   

<details>
<summary>Code</summary>

```java
public class Solution {
    public int solve(ArrayList<Integer> A, ArrayList<Integer> B) {
        int n = A.size();
        int ans = Integer.MAX_VALUE;
        // Loop for j(middle) values and find right i(left) & k(right) values
        for(int j=1;j<n-1;j++){
           
            int tmp_cost=B.get(j); int iValue=Integer.MAX_VALUE; int kValue=Integer.MAX_VALUE;

            for(int i=j-1; i>=0; i--){
                if(A.get(i)<A.get(j) && B.get(i)<iValue){
                    iValue = Math.min(iValue, B.get(i));
                }
            }

            for(int k=j+1; k<n; k++){
                if(A.get(k)>A.get(j) && B.get(k)<kValue){
                    kValue = Math.min(kValue, B.get(k));
                }
            }

            if(iValue != Integer.MAX_VALUE && kValue != Integer.MAX_VALUE){
               tmp_cost += iValue+kValue;
               ans = Math.min(ans, tmp_cost);
            }

        }

        if(ans != Integer.MAX_VALUE){
            return ans;
        } else {
            return -1;
        }
    }
}

```
 </details> 
