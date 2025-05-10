[GoBack](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Bits/03%20Uses.md)
### **Checking Even/Odd Using the Bitwise AND (`&`) Operator** 🚀

In binary, **even numbers always end in `0`**, and **odd numbers always end in `1`**. We can use the **bitwise AND (`&`) operator** to quickly check whether a number is even or odd.

----------

### **🚀 Concept**

-   Every **odd number** has its **last bit as `1`**.
-   Every **even number** has its **last bit as `0`**.
-   If we perform `num & 1`, it will return:
    -   `0` → **Even number** (last bit is `0`).
    -   `1` → **Odd number** (last bit is `1`).

----------

### **📝 Code Example**

```java
public class EvenOddChecker {
    public static void main(String[] args) {
        int num = 7; // Try changing this to an even or odd number

        if ((num & 1) == 0) {
            System.out.println(num + " is Even");
        } else {
            System.out.println(num + " is Odd");
        }
    }
}

```

----------

### **🔍 Explanation**

Let's take `7` and `8` as examples:

#### **Binary Representation**

-   `7` → `0111` (Last bit is `1`, so odd)
-   `8` → `1000` (Last bit is `0`, so even)

Performing `num & 1`:

```
7 & 1 = 0111 & 0001 = 0001 (Result = 1 → Odd)
8 & 1 = 1000 & 0001 = 0000 (Result = 0 → Even)

```

Since the last bit determines **even or odd**, this method is **faster than using modulus (`%`)** because bitwise operations are **extremely efficient**.

----------

### **🛠️ Why Use Bitwise Instead of `%`?**

-   **Efficiency**: `&` is faster than `%`, especially for large computations.
-   **Low-Level Optimization**: Used in embedded systems, OS-level programming, and bitwise tricks.

[GoBack](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Bits/03%20Uses.md)
