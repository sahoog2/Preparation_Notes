[GoBack](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Bits/03%20Uses.md)
### **Division by Powers of 2 Using Bit Masking** 🚀  

Dividing a number by a power of `2` can be done **efficiently** using **bitwise right shift (`>>`)**, instead of traditional division (`/`).

---

### **📌 Key Idea**
✅ **Shifting bits right by `k` positions** divides a number by `2^k`.  
✅ **Formula:**
```math
N ÷ 2^k  =  N >> k
```
✅ **Why It Works?**  
Each right shift moves all bits **one position to the right**, effectively **halving** the number for each shift.

---

### **🚀 Example Code in Java**
```java
public class BitwiseDivision {
    public static void main(String[] args) {
        int num = 40; // Number to divide
        int power = 3; // Divide by 2^3 (i.e., 8)

        int result = num >> power; // Equivalent to 40 / 8
        System.out.println("Result: " + result); // Output: 5
    }
}
```
**Explanation:**
- `40` → Binary: `0010 1000`
- `40 >> 3` shifts bits right by `3` positions:
```
0010 1000  →  Original (40)
↓ Right shift (3 positions)
0000 0101  →  Result (5)
```

---

### **🔥 Why Use Bitwise Shifting for Division?**
✅ **Faster** than traditional division (`/`) in low-level computations.  
✅ **Optimized for performance-critical applications (graphics, networking).**  
✅ **Used in efficient algorithms for image processing and cryptography.**  

Would you like insights into signed vs. unsigned right shifts (`>>` vs. `>>>`)? 
[GoBack](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Bits/03%20Uses.md)
