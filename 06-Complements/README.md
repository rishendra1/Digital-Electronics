# Complements in Digital Systems

## Overview
Complements are used in digital systems to simplify subtraction operations and represent signed numbers. They convert subtraction into addition, making hardware implementation simpler.

## Why Complements?

### Advantages
- **Simplify Subtraction**: A - B = A + (-B)
- **Unified Hardware**: Same adder circuit for both operations
- **Signed Number Representation**: Elegant way to represent negative numbers
- **No Separate Subtractor**: Reduces circuit complexity
- **Overflow Detection**: Easy to detect

## Types of Complements

For base-r number system:
1. **r's Complement** (Radix complement)
2. **(r-1)'s Complement** (Diminished radix complement)

### For Binary (r=2):
- **2's Complement**
- **1's Complement**

### For Decimal (r=10):
- **10's Complement**
- **9's Complement**

## 1's Complement

### Definition
Invert all bits: 0 → 1, 1 → 0

### How to Find
**Method 1:** Flip each bit
**Method 2:** Subtract from (2ⁿ - 1) where n = number of bits

### Examples

**Example 1:**
```
Binary: 1011
1's Comp: 0100
```

**Example 2:**
```
Binary: 10110101
1's Comp: 01001010
```

**Example 3:**
```
Binary: 11111111
1's Comp: 00000000
```

### Properties
- Simple to implement (just NOT gate)
- Two representations for zero:
  - +0 = 0000
  - -0 = 1111
- Used in early computers
- Symmetric around zero

### Signed Number Representation (1's Complement)

**For n-bit numbers:**
- Range: -(2ⁿ⁻¹ - 1) to +(2ⁿ⁻¹ - 1)
- **4-bit range**: -7 to +7
- **8-bit range**: -127 to +127

**Sign bit:**
- MSB = 0 → Positive
- MSB = 1 → Negative

| Decimal | 4-bit 1's Comp |
|---------|----------------|
| +7      | 0111           |
| +6      | 0110           |
| +5      | 0101           |
| +4      | 0100           |
| +3      | 0011           |
| +2      | 0010           |
| +1      | 0001           |
| +0      | 0000           |
| -0      | 1111           |
| -1      | 1110           |
| -2      | 1101           |
| -3      | 1100           |
| -4      | 1011           |
| -5      | 1010           |
| -6      | 1001           |
| -7      | 1000           |

### Arithmetic with 1's Complement

**Addition:**
1. Add binary numbers
2. If carry out, add it to LSB (end-around carry)

**Example 1: 6 + 3**
```
  0110 (+6)
+ 0011 (+3)
-------
  1001 (+9)
```

**Example 2: 6 + (-3)**
```
  0110 (+6)
+ 1100 (-3)
-------
 1 0010
+     1  ← End-around carry
-------
  0011 (+3)
```

**Example 3: -6 + (-3)**
```
  1001 (-6)
+ 1100 (-3)
-------
 1 0101
+     1  ← End-around carry
-------
  0110 (-9 incorrect!)
  
Actual: 1001 = -6 (error in example)
```

## 2's Complement

### Definition
2's Complement = 1's Complement + 1

### How to Find

**Method 1:** Invert all bits and add 1
```
Number:    1011
1's Comp:  0100
Add 1:   +    1
2's Comp:  0101
```

**Method 2:** Starting from right, keep bits until first 1, then invert rest
```
Number:   10110100
          ↓
Keep-->   00
Flip-->   01001100
2's Comp: 01001100
```

### Examples

**Example 1:**
```
Binary:   0011
1's Comp: 1100
Add 1:  +    1
2's Comp: 1101
```

**Example 2:**
```
Binary:   10000000
1's Comp: 01111111
Add 1:  +        1
2's Comp: 10000000
(Special case: -128 in 8-bit)
```

### Properties
- **Most widely used** in modern computers
- **One representation for zero**: 0000 only
- **Asymmetric range**: One more negative number
- Simpler arithmetic (no end-around carry)
- Direct hardware implementation

### Signed Number Representation (2's Complement)

**For n-bit numbers:**
- Range: -2ⁿ⁻¹ to +(2ⁿ⁻¹ - 1)
- **4-bit range**: -8 to +7
- **8-bit range**: -128 to +127
- **16-bit range**: -32768 to +32767

| Decimal | 4-bit 2's Comp |
|---------|----------------|
| +7      | 0111           |
| +6      | 0110           |
| +5      | 0101           |
| +4      | 0100           |
| +3      | 0011           |
| +2      | 0010           |
| +1      | 0001           |
|  0      | 0000           |
| -1      | 1111           |
| -2      | 1110           |
| -3      | 1101           |
| -4      | 1100           |
| -5      | 1011           |
| -6      | 1010           |
| -7      | 1001           |
| -8      | 1000           |

### Arithmetic with 2's Complement

**Addition:**
1. Add binary numbers
2. Discard carry out (if any)
3. Check for overflow

**Example 1: 6 + 3**
```
  0110 (+6)
+ 0011 (+3)
-------
  1001 (+9)
No overflow
```

**Example 2: 6 + (-3)**
```
  0110 (+6)
+ 1101 (-3)
-------
 1 0011  ← Discard carry
  0011 (+3) ✓
```

**Example 3: -6 + (-3)**
```
  1010 (-6)
+ 1101 (-3)
-------
 1 0111  ← Discard carry
  0111 (+7) ✗ OVERFLOW!

Correct answer should be -9
But 4-bit range is only -8 to +7
```

**Subtraction: A - B**
1. Find 2's complement of B
2. Add: A + (-B)

**Example: 9 - 4**
```
9 = 1001
4 = 0100
-4 = 1100 (2's comp)

  1001 (+9)
+ 1100 (-4)
-------
 1 0101  ← Discard carry
  0101 (+5) ✓
```

### Overflow Detection

**When does overflow occur?**
- Adding two positive numbers → negative result
- Adding two negative numbers → positive result

**Detection Methods:**

1. **Sign Bit Method:**
   - If sign(A) = sign(B) ≠ sign(Sum) → Overflow

2. **Carry Method:**
   - If C(n) ⊕ C(n-1) = 1 → Overflow
   - C(n) = carry out of MSB
   - C(n-1) = carry into MSB

**Examples:**

**Overflow Example:**
```
  0110 (+6)
+ 0101 (+5)
-------
  1011 (-5) ✗ OVERFLOW
Expected: +11, Got: -5
```

**No Overflow Example:**
```
  0110 (+6)
+ 1101 (-3)
-------
 1 0011 (+3) ✓ No overflow
```

## Comparison: 1's vs 2's Complement

| Feature | 1's Complement | 2's Complement |
|---------|----------------|----------------|
| Zero representation | Two (+0, -0) | One (0) |
| Range (n-bit) | -(2ⁿ⁻¹-1) to +(2ⁿ⁻¹-1) | -2ⁿ⁻¹ to +(2ⁿ⁻¹-1) |
| Finding complement | Invert bits | Invert + 1 |
| Addition | End-around carry | Discard carry |
| Hardware | Slightly complex | Simpler |
| Usage | Legacy systems | Modern computers |
| Symmetry | Symmetric | Asymmetric |

## Sign Extension

**Purpose:** Convert n-bit number to m-bit (m > n) while preserving value

**Rule:** Replicate the sign bit

**Examples:**

```
4-bit to 8-bit:
+5:  0101 → 00000101
-3:  1101 → 11111101
```

```
8-bit to 16-bit:
+42:  00101010 → 0000000000101010
-10:  11110110 → 1111111111110110
```

## Decimal Complements

### 9's Complement
Subtract each digit from 9

**Example:**
```
Number:    4672
9's Comp:  5327
(9-4)(9-6)(9-7)(9-2)
```

### 10's Complement
10's Complement = 9's Complement + 1

**Example:**
```
Number:     4672
9's Comp:   5327
Add 1:    +    1
10's Comp:  5328
```

## Applications

### 1. Signed Integer Representation
- All programming languages use 2's complement
- C/C++, Java, Python integers

### 2. Subtraction Circuits
- ALU (Arithmetic Logic Unit)
- Microprocessors
- Digital calculators

### 3. Negative Number Storage
- Memory systems
- Registers
- Data transmission

### 4. Comparison Operations
- Greater than, less than
- Equality checks

## Important Notes

- **2's complement is standard** in modern systems
- **Only one zero** in 2's complement (major advantage)
- **Overflow** must be detected in signed arithmetic
- **Sign bit** determines positive/negative
- **Subtraction** becomes addition with complement
- **Hardware simplification** is key benefit
- Range is **asymmetric** in 2's complement

## Common Mistakes to Avoid

1. ❌ Forgetting to add 1 for 2's complement
2. ❌ Not handling end-around carry in 1's complement
3. ❌ Ignoring overflow in addition
4. ❌ Wrong sign extension
5. ❌ Confusing 1's and 2's complement
6. ❌ Not discarding final carry in 2's complement addition

## Quick Reference

### Finding 2's Complement:
```
Method 1: NOT + 1
Method 2: Copy from right until first 1, then invert
```

### Subtraction:
```
A - B = A + (2's comp of B)
```

### Overflow Detection:
```
Positive + Positive = Negative → Overflow
Negative + Negative = Positive → Overflow
```

## Resources

- Reference: Digital Design by M. Morris Mano (Chapter 1)
- Practice complement arithmetic regularly
- Understand hardware implementation
- Study overflow conditions thoroughly
