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

Would you like more variations such as **Modular Inverse Using Fast Power**? 🚀
[GoBack](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Bits/03%20Uses.md)
