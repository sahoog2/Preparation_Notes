### **Multiplication by Powers of 2 Using Bit Masking** 🚀  

Multiplying a number by powers of `2` can be done efficiently using **bitwise left shift (`<<`)**, rather than traditional multiplication operations.

---

### **📌 Key Idea**
✅ In binary, shifting bits **left** by `k` positions multiplies a number by `2^k`.  
✅ **Formula:**  
```math
N × 2^k  =  N << k
```
✅ **Why It Works?**  
Each left shift moves all bits to the left, effectively **doubling** the number for each shift.

---

### **🚀 Example Code in Java**
```java
public class BitwiseMultiplication {
    public static void main(String[] args) {
        int num = 5; // Number to multiply
        int power = 3; // Multiply by 2^3 (i.e., 8)

        int result = num << power; // Equivalent to 5 * 8
        System.out.println("Result: " + result); // Output: 40
    }
}
```
**Explanation:**
- `5` → Binary: `0000 0101`
- `5 << 3` shifts bits left by 3 positions:
```
0000 0101  →  Original (5)
↓ Left shift (3 positions)
0010 1000  →  Result (40)
```

---

### **🔥 Why Use Bitwise Shifting for Multiplication?**
✅ **Faster** than traditional multiplication (`*`).  
✅ **Optimized for low-level operations (embedded systems, cryptography).**  
✅ **Used in performance-critical applications (image processing, graphics, networking).**  

Would you like a deep dive into bitwise tricks for division and modular arithmetic? 🚀
