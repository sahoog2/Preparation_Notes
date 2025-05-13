Bitwise operators are incredibly powerful and efficient for solving a variety of computational problems. Below is an **exhaustive list** of problems that can be tackled using bitwise operations:

----------

### **1. Basic Number Operations**
---
✅ [**Checking Even/Odd**](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Bits/OddEven.md): `(n & 1) == 0` → Even, otherwise Odd  
✅ [**Swapping Two Numbers Without Temporary Variable**](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Bits/Swap%20Numbers.md):

```java
a = a ^ b;
b = a ^ b;
a = a ^ b;

```

✅ [**Multiplication by Powers of 2**](https://github.com/sahoog2/Preparation_Notes/blob/main/DSA/Bits/Multiplication%20by%20Powers%20of%202.md): `n << k` → `n * 2^k`  
✅ **Division by Powers of 2**: `n >> k` → `n / 2^k`  
✅ **Checking if a Number is a Power of 2**: `(n & (n - 1)) == 0`

----------

### **2. Bit Manipulation & Optimization**

✅ **Set a Particular Bit**: `num |= (1 << position)`  
✅ **Clear a Particular Bit**: `num &= ~(1 << position)`  
✅ **Toggle a Bit**: `num ^= (1 << position)`  
✅ **Counting Set Bits (`Hamming Weight`)**:

```java
while (n > 0) {
    count += (n & 1);
    n >>= 1;
}

```

✅ **Fast Exponentiation (Binary Exponentiation)**  
✅ **Reverse Bits of an Integer**

----------

### **3. Boolean & Bitmask Operations**

✅ **Bitwise AND, OR, XOR for Boolean Computations**  
✅ **Using Bit Masks for Permissions & Flags**  
✅ **Checking if Two Numbers Have Opposite Signs**: `(x ^ y) < 0`

----------

### **4. Mathematical & Algorithmic Problems**

✅ **Finding the Unique Element in an Array (XOR property)**  
✅ **Finding Two Missing Numbers in an Array Using XOR**  
✅ **Finding the Single Non-Repeated Number in a Duplicate Array**  
✅ **Fast Fibonacci Calculation Using Matrix Exponentiation**  
✅ **Fast Greatest Common Divisor (GCD) Using Bitwise Operations**

----------

### **5. Graphics & Image Processing**
---
✅ **Bitwise Operations for Alpha Blending**  
✅ **Bitwise Operations for Edge Detection (Sobel Operator)**  
✅ **Image Compression Using Bitwise Techniques**

----------

### **6. Cryptography & Security**

✅ **Efficient Hashing Algorithms**  
✅ **Bitwise Operations in Encryption (AES, RSA)**  
✅ **Parity Check in Error Detection & Correction**

----------

### **7. Data Compression**

✅ **Run-Length Encoding**  
✅ **Huffman Coding for Compression**  
✅ **Efficient Representation of Sparse Data Structures**

----------

### **8. System-Level Computation**

✅ **Efficient Scheduling Using Bit Masks**  
✅ **Memory Addressing & Alignment in Low-Level Programming**  
✅ **Network Subnet Mask Calculation Using Bitwise Operations**

----------

💡 **Final Thoughts:**  
Bitwise operations are **extremely efficient** and provide **low-level control** over computations. They are **widely used in performance-critical applications** like gaming engines, cryptography, and embedded systems.
