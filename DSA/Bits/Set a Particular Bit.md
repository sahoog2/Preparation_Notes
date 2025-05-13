[GoBack](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Bits/03%20Uses.md)
### **Setting a Particular Bit Using Bit Masking** 🚀  

Setting a specific bit in a number means **turning that bit to `1`** while **keeping all other bits unchanged**. We achieve this using the **bitwise OR (`|`) operator** with a mask.

---

### **📌 Key Idea**
✅ **Use a bit mask:**  
   - Create a mask where only the desired bit is **set (`1`)**, all others **remain `0`**.  
   - Use the **OR (`|`)** operator to merge the mask into the original number.  

✅ **Formula to Set Bit at Position `k`**:  
```math
num |= (1 << k)
```
- **`1 << k`** → Creates a mask with only the `k-th` bit set.  
- **OR (`|`) merges the mask with the original number**.  

---

### **🚀 Optimized Code in Java**
```java
public class BitwiseSetBit {
    public static int setBit(int num, int k) {
        return num | (1 << k);
    }

    public static void main(String[] args) {
        int num = 5;  // Binary: 0000 0101
        int k = 1;     // Set the 1st bit

        int result = setBit(num, k);
        System.out.println("Updated Number: " + result); // Output: 7 (Binary: 0000 0111)
    }
}
```

---

### **🔍 Explanation**
Let’s say `num = 5` (`0000 0101`) and we want to **set the 1st bit**:

1️⃣ **Create the mask** (`1 << 1` → `0000 0010`)  
2️⃣ **OR (`|`) operation**:
```
  0000 0101   (num = 5)
| 0000 0010   (mask for 1st bit)
--------------
  0000 0111   (Updated num = 7)
```
Since OR (`|`) keeps `1` wherever **either operand is `1`**, it **sets the bit while preserving other bits**.

---

### **🔥 Why Is This Efficient?**
✅ **Runs in O(1) time** → Just one bitwise operation.  
✅ **No loops or extra variables** → Works instantly.  
✅ **Optimized for embedded systems, networking, cryptography, and low-level programming**.  

Would you like bit masking tricks for **clearing or toggling bits**? 🚀

[GoBack](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Bits/03%20Uses.md)
