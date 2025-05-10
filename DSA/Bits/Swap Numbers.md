[GoBack](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Bits/03%20Uses.md)

Swapping two numbers without using a temporary variable is a **classic bitwise trick** that leverages the **XOR (`^`) operator**.

### **🚀 Concept**

-   The **XOR (`^`) operator** works by comparing bits:
    -   `1 ^ 1 = 0` (same bits → 0)
    -   `0 ^ 0 = 0` (same bits → 0)
    -   `1 ^ 0 = 1` (different bits → 1)

### **📝 Code Example**

```java
public class SwapNumbers {
    public static void main(String[] args) {
        int a = 5, b = 7;

        System.out.println("Before swap: a = " + a + ", b = " + b);

        // Swap using XOR
        a = a ^ b;
        b = a ^ b;
        a = a ^ b;

        System.out.println("After swap: a = " + a + ", b = " + b);
    }
}

```

----------

### **🔍 Step-by-Step Explanation**

Let's take `a = 5` and `b = 7`:

#### **Binary Representation**

-   `5` → `0101`
-   `7` → `0111`

✅ **Step 1: `a = a ^ b`**

```
    0101  (5)
^   0111  (7)
--------------
    0010  (Result → a = 2)

```

✅ **Step 2: `b = a ^ b`**

```
    0010  (Now a = 2)
^   0111  (7)
--------------
    0101  (Result → b = 5)

```

✅ **Step 3: `a = a ^ b`**

```
    0010  (Now a = 2)
^   0101  (Now b = 5)
--------------
    0111  (Result → a = 7)

```

🎉 **Final Swap** → `a = 7, b = 5` ✅

----------

### **💡 Why Use XOR Instead of Temporary Variable?**

-   **Saves Memory** (No extra storage required).
-   **Works Efficiently** (Only requires bitwise operations).
-   **Avoids Additional Assignments**.

[GoBack](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Bits/03%20Uses.md)
