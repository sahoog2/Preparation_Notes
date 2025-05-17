#  Amazing Subarrays

[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25458/homework/problems/1054/hints?navref=cl_pb_nv_tb)
[Solution](#Solution)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)

You are given a string  **S**, and you have to find all the  **amazing substrings**  of  **S**.

An amazing Substring is one that starts with a  **vowel**  (a, e, i, o, u, A, E, I, O, U).

**Input**

```
Only argument given is string S.

```

**Output**

```
Return a single integer X mod 10003, here X is the number of Amazing Substrings in given the string.

```

**Constraints**

```
1 <= length(S) <= 1e6
S can have special characters

```

**Example**

```
Input
    ABEC

Output
    6

Explanation
    Amazing substrings of given string are :
    1. A
    2. AB
    3. ABE
    4. ABEC
    5. E
    6. EC
    here number of substrings are 6 and 6 % 10003 = 6.
```




[Use Hint](https://www.scaler.com/academy/mentee-dashboard/class/25458/homework/problems/1054/hints?navref=cl_pb_nv_tb)
[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)

# Solution
The main idea to solve this problem is to traverse the string and when you encounter a vowel, add **( length(string) - position_of_curr_char )** to the answer.

```java
import java.util.*;

  

public  class Solution {

public  int solve(String A)  {

int ans =  0;

int n = A.length();

  

Set<Character> vowel =  new HashSet<>(Arrays.asList('A','E','I','O','U','a','e','i','o','u'));

  

for(int i=0; i<n; i++){

if(vowel.contains(A.charAt(i))){

ans =  (ans +  (n-i))%10003;

}

}

  

return ans%10003;

}

}
```

[Go Back](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Array/2%20Problems.md)
