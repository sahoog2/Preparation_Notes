[GoBack](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Bits/03%20Uses.md)
### **Fast Exponentiation Using Bitmasking (Binary Exponentiation)** 🚀  

**Fast Exponentiation** (or **Binary Exponentiation**) is an efficient method to compute **`a^b`** in `O(log b)` time instead of `O(b)`. It leverages **bitwise operations** for optimized power calculations.

---

### **📌 Key Idea**
✅ **Exponentiation by Squaring**: Breaks `b` into binary form, reducing multiplications.  
✅ **Use Bit Masking (`&`)** to check if a bit is set (`1`) in the exponent.  
✅ **Multiply when a bit is set, square otherwise** → Keeps calculations minimal.  

---

### **🚀 Optimized Code in Java**
```java
public class FastExponentiation {
    public static long fastPower(long base, long exp, long mod) {
        long result = 1;

        while (exp > 0) {
            // If the current bit in 'exp' is set, multiply the base
            if ((exp & 1) == 1) {
                result = (result * base) % mod;
            }
            // Square the base and shift the exponent right
            base = (base * base) % mod;
            exp >>= 1; // Divide exponent by 2 using bitwise shift
        }
        return result;
    }

    public static void main(String[] args) {
        System.out.println(fastPower(2, 10, 1000000007)); // Output: 1024
    }
}
```

---

### **🔍 Explanation**
Let’s compute `2^10` using **Binary Exponentiation**:

1️⃣ **Binary representation of `10`** → `1010`  
2️⃣ **Loop through bits**, multiplying only when the bit is `1`.  
3️⃣ **Use right shift (`>>`)** to efficiently process the exponent.  

✅ **Time Complexity:** `O(log b)`  
✅ **Space Complexity:** `O(1)`  

---

### **🔥 Why Use This Method?**
✅ **Super fast** (`O(log b)` vs. `O(b)`).  
✅ **Optimized for cryptography and modular arithmetic (`mod m`).**  
✅ **Used in RSA encryption, large number computations, and competitive programming.**  

[GoBack](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Bits/03%20Uses.md)

## **Choosing the Right Modulus (`mod`) for a Problem** 🚀

The **modulus (`mod`) value** in a problem is selected based on the **problem constraints** and the nature of calculations involved. Here’s how to decide:


### **📌 General Guidelines for Selecting `mod`**

✅ **Prevent Overflow** → Large calculations need a modulus to keep values manageable.  
✅ **Prime Numbers (`mod`)** → Common choices in **cryptography** and **number theory**.  
✅ **Competitive Programming Standards** → Frequently used **mod values** for coding challenges:

-   `10^9 + 7` (`1000000007`) → Large prime, used in modular arithmetic.
-   `998244353` → Another commonly used prime modulus.

### **🚀 Key Considerations Based on Use Case**

✅ **Cryptography** → Use **large prime numbers** to ensure security (`mod` in RSA).  
✅ **Number Theory & Modular Arithmetic** → If finding **remainders**, choose `mod` relative to divisor constraints.  
✅ **Graph & Combinatorics Problems** → Use **prime mod values** for easier modular inverse calculations.  
✅ **Optimizing Exponentiation** → Select a `mod` that simplifies **`a^b mod m`** using **fast exponentiation**.

----------

### **🔥 Example Scenarios**

1️⃣ **Finding remainders of division**

```math
A % M = B % M

```

Choose `mod = M`, based on constraints in the problem.

2️⃣ **Solving equations using modular inverse**

```math
(A / B) % mod = (A * B⁻¹) % mod

```

Choose a **prime modulus** so that `B⁻¹` (modular inverse) exists.

3️⃣ **Reducing large number computations**

```math
(A * B) % mod

```

Choose `mod = 10^9 + 7` for standard programming problems.

----------

### **💡 Summary**
| Problem Type | Recommended `mod` |
|--|--|
| Large number computations |`10^9 + 7`  |
|Cryptography (RSA, ECC)|Large **prime numbers** |
|Graph Algorithms & Combinatorics|`998244353` (large prime)|
|Basic remainder problems|Given divisor (`M`)|


[GoBack](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Bits/03%20Uses.md)
