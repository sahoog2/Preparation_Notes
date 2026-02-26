

[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25464/assignment/problems/4256/hints?navref=cl_pb_nv_tb)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)

<details>
<summary>**Problem Description**</summary>

Given a binary string  **A**. It is allowed to do at most one swap between any 0 and 1. Find and return the length of the longest consecutive 1’s that can be achieved.

  
**Input Format**

```
The only argument given is string A.

```

**Output Format**

```
Return the length of the longest consecutive 1’s that can be achieved.

```

**Constraints**

```
1 <= length of string <= 1000000
A contains only characters 0 and 1.

```

**For Example**

```
Input 1:
    A = "111000"
Output 1:
    3

Input 2:
    A = "111011101"
Output 2:
    7
```
</details>

<details>
<summary>Approach</summary>

Create two arrays which store the number of consecutive ones on the right and left of all indexes.

Now, for each index x having character ‘0’, the answer will be the maximum of answer and left consecutive ones of (x-1) + right consecutive ones of (x+1) + 1 if there is extra 1 other then these, else left consecutive ones of (x-1) + right consecutive ones of (x+1)

**Time Complexity : O(n)**  
**Space Complexity : O(n)**
</details>   

<details>
<summary>Code</summary>

```java
public int solve(String A) {
        int n = A.length();
        int oneCount = 0; //total number of 1 in the string/array
        int[] lA = new int[n]; //array containing max consecutive 1 to the left of i
        int[] rA = new int[n]; //array containing max consecutive 1 to the right of i

        // counting total number of 1
        for(int i=0;i<n;i++){
            if(A.charAt(i)=='1'){
                oneCount++;
            }
        }

        //computing lA
        for(int i=0;i<n;i++){  
            // here we need to check for value "1" at i and update. 
            // as by default java initalize the array with default value as 0.  
            if(i==0){
                // We need to take care of 0th position to avoid arrayOutObBound exception 
                // in the formula used in else part. 
                if(A.charAt(i)=='1'){ 
                    lA[i] = 1;
                }
            } else if(A.charAt(i)=='1'){
                // here we are checking if A[i] value is 1 and adding 1 to 
                // previous consecutive 1's count accordingly.
                lA[i] = lA[i-1] + 1; 
            }
        }

        //computing rA
        for(int i=n-1;i>=0;i--){ 
            // here we need to check for value "1" at i and update 
            // as by default java initalize the array with default value as 0.   
            if(i==n-1){ 
                // We need to take care of n-1 th position to avoid arrayOutObBound exception 
                // in the formula used in else part.
                if(A.charAt(i)=='1'){
                    rA[i] = 1;
                }
            } else if(A.charAt(i)=='1'){
                // here we are checking if A[i] value is 1 and adding 1 to next consecutive 1 count accordingly.
                rA[i] = rA[i+1] + 1; 
            }
        }

        int maxCnt = 0;

        // need to calculate maxCnt for boundary positions as 
        // the formula wont be handling 0th and n-1 th position
        // to avoid arrayOutObBound exception
        for(int i=0;i<n;i++){
            maxCnt = Math.max(maxCnt, Math.max(lA[i], rA[i]));
        }    
        for(int i=1;i<n-1;i++){
            int cnt = 0;
            if(A.charAt(i)=='0'){
                // here we are counting max consecutive 1 at i by adding 
                // max consecutive to its left and max consecutive to its right 
                cnt = lA[i-1] + rA[i+1];

                // here we are checking if cnt is less than total no of 1
                // if it is less, which means there is one extra 1 which can be swapped with this 0
                // so max consecutive 1 length will be increased by 1.
                if(cnt < oneCount){
                    cnt++;
                }

            }

            maxCnt = Math.max(maxCnt, cnt);
            
        }

        return maxCnt;

    }

```
 </details> 
