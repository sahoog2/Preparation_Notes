[GoBack](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Bits/03%20Uses.md)
### **Checking if a Number is a Power of 2 Using Bitmasking** 🚀  

A number `N` is a **power of 2** if **it has exactly one bit set** in its binary representation. That means:
✅ Powers of 2 → `1, 2, 4, 8, 16, 32, ...`  
✅ Their binary forms → `0001, 0010, 0100, 1000, 10000, ...`  

---

### **📌 Key Idea**
If `N` is a power of `2`, then **`N & (N - 1) == 0`**  
✅ **Why?**  
For any power of `2`, `N-1` has all bits set **after** the highest `1`-bit:
```
N     =  00010000  (16)
N-1   =  00001111  (15)
```
Bitwise AND (`&`) will result in **zero** (`00000000`), confirming `N` is a power of 2.

---

### **🚀 Optimized Code in Java**
```java
public class PowerOfTwoChecker {
    public static boolean isPowerOfTwo(int num) {
        return num > 0 && (num & (num - 1)) == 0;
    }

    public static void main(String[] args) {
        int num = 16;
        System.out.println(num + " is a power of 2? " + isPowerOfTwo(num)); // Output: true
    }
}
```

---

### **🔥 Why Is This Efficient?**
✅ **Runs in O(1) time** → Just one bitwise operation.  
✅ **No loops or recursion** → Works instantly.  
✅ **Handles large numbers efficiently** without complex division operations.  

Would you like more bitwise tricks for number properties? 🚀
[GoBack](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Bits/03%20Uses.md)
