
## **1. Bitwise AND (`&`)**

-   The **AND** operator sets a bit to `1` **only if both bits are `1`**.

🚀 **Example:**

```java
int a = 5;  // 0101 in binary
int b = 3;  // 0011 in binary
int result = a & b; // 0001 (1 in decimal)
System.out.println(result); // Output: 1

```

**Explanation:**

-   `5` = `0101`
-   `3` = `0011`
-   Applying `&`:

```
0101
0011
------
0001  (Result = 1)

```

Only the **rightmost bit matches**, so the result is **1**.

----------

## **2. Bitwise OR (`|`)**

-   The **OR** operator sets a bit to `1` **if at least one operand’s bit is `1`**.

🚀 **Example:**

```java
int a = 5;  // 0101
int b = 3;  // 0011
int result = a | b; // 0111 (7 in decimal)
System.out.println(result); // Output: 7

```

**Explanation:**

```
0101
0011
------
0111  (Result = 7)

```

Any `1` in either operand **stays `1`**.

----------

## **3. Bitwise XOR (`^`)**

-   **Exclusive OR (XOR)** sets a bit to `1` **if the bits are different**.

🚀 **Example:**

```java
int a = 5;  // 0101
int b = 3;  // 0011
int result = a ^ b; // 0110 (6 in decimal)
System.out.println(result); // Output: 6

```

**Explanation:**

```
0101
0011
------
0110  (Result = 6)

```

Only where the bits **differ**, the result is **1**.

----------

## **4. Bitwise NOT (`~`)**

-   **Flips all bits** (`1` → `0`, `0` → `1`).  
    🚀 **Example:**

```java
int a = 5;  // 0101
int result = ~a;  // Inverts bits
System.out.println(result); // Output: -6 (Two’s complement)

```

**Explanation:**

-   In Java, negative numbers are stored in **two’s complement notation**, so `~5` results in `-6`.

----------

## **5. Left Shift (`<<`)**

-   **Shifts bits left**, effectively multiplying by `2` per shift.

🚀 **Example:**

```java
int a = 5;  // 0000 0101
int result = a << 1;  // Shift left by 1 position
System.out.println(result); // Output: 10

```

**Explanation:**

```
0000 0101  (5)
↓ Shift left
0000 1010  (10)

```

Each shift **doubles the value**.

----------

## **6. Right Shift (`>>`)**

-   **Shifts bits right**, effectively dividing by `2` per shift.

🚀 **Example:**

```java
int a = 10;  // 0000 1010
int result = a >> 1;  // Shift right by 1 position
System.out.println(result); // Output: 5

```

**Explanation:**

```
0000 1010  (10)
↓ Shift right
0000 0101  (5)

```

Each shift **halves the value**.

----------

## **7. Unsigned Right Shift (`>>>`)**

-   Works like `>>`, but **fills with `0`** instead of preserving the sign for negative numbers.

🚀 **Example:**

```java
int a = -10;  // Negative number in two's complement
int result = a >>> 1;  // Shift right
System.out.println(result);

```

If you need **logical shifting**, `>>>` ensures the leftmost bit **doesn’t stay negative**.

----------
