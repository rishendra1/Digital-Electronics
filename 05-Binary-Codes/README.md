# Binary Codes

## Overview
Binary codes are used to represent information in digital systems. Different coding schemes serve different purposes - data representation, error detection, arithmetic operations, and more.

## Classification of Binary Codes

### 1. Weighted Codes
- Each bit position has a specific weight
- Examples: BCD (8421), 2421, 5211

### 2. Non-Weighted Codes
- No specific weights assigned to positions
- Examples: Excess-3, Gray code

### 3. Error Detecting Codes
- Detect errors in data transmission
- Examples: Parity codes, Hamming code

### 4. Error Correcting Codes
- Detect AND correct errors
- Examples: Hamming code, CRC

## Binary Coded Decimal (BCD)

### 8421 BCD Code

**Features:**
- Most commonly used BCD code
- Each decimal digit represented by 4 bits
- Weights: 8-4-2-1
- Also called Natural BCD

**Valid Codes:** 0000 to 1001 (0 to 9)
**Invalid Codes:** 1010 to 1111 (10 to 15)

**Decimal to BCD Table:**

| Decimal | BCD (8421) |
|---------|------------|
| 0       | 0000       |
| 1       | 0001       |
| 2       | 0010       |
| 3       | 0011       |
| 4       | 0100       |
| 5       | 0101       |
| 6       | 0110       |
| 7       | 0111       |
| 8       | 1000       |
| 9       | 1001       |

**Example:**
- Decimal: 247
- BCD: 0010 0100 0111
- Binary: 11110111 (different!)

### BCD Addition

**Rules:**
1. Add BCD digits normally
2. If sum ≤ 9 and no carry → Result is valid BCD
3. If sum > 9 OR carry generated → Add 0110 (6) to sum
4. Propagate carry to next digit

**Example: 25 + 13**
```
    2    5
  0010 0101
+ 0001 0011
-----------
  0011 1000  ← Valid (3 8)
```

**Example: 67 + 58**
```
    6    7
  0110 0111
+ 0101 1000
-----------
  1011 1111  ← Invalid (11 15)
+ 0110 0110  ← Add 6 to both
-----------
  0010 0101  ← Result with carry
     1        ← Carry = 1
Answer: 125
```

### Advantages of BCD
- Easy conversion to/from decimal
- Simple for human readability
- Used in calculators, digital clocks
- No conversion errors

### Disadvantages of BCD
- Requires more bits than pure binary
- Arithmetic operations more complex
- Waste of 6 combinations (1010-1111)
- Inefficient storage

## Gray Code

### Features
- **Non-weighted code**
- **Unit distance code**: Adjacent numbers differ by only ONE bit
- **Reflective code**: Symmetric pattern
- **Cyclic code**: Last and first codes differ by one bit

### Binary to Gray Code Conversion

**Method:**
1. MSB of Gray = MSB of Binary
2. XOR each binary bit with previous bit

**Formula:**
- G(n) = B(n) ⊕ B(n+1)

**Example: Binary 1011 → Gray**
```
Binary: 1  0  1  1
Gray:   1  1  1  0
        ↓  ↑  ↑  ↑
        1⊕0=1 0⊕1=1 1⊕1=0
```

### Gray to Binary Conversion

**Method:**
1. MSB of Binary = MSB of Gray
2. XOR this bit with next Gray bit
3. Continue for all bits

**Example: Gray 1110 → Binary**
```
Gray:   1  1  1  0
Binary: 1  0  1  1
        ↓  ↑  ↑  ↑
        1  1⊕1=0 0⊕1=1 1⊕0=1
```

### Gray Code Table (4-bit)

| Decimal | Binary | Gray |
|---------|--------|------|
| 0       | 0000   | 0000 |
| 1       | 0001   | 0001 |
| 2       | 0010   | 0011 |
| 3       | 0011   | 0010 |
| 4       | 0100   | 0110 |
| 5       | 0101   | 0111 |
| 6       | 0110   | 0101 |
| 7       | 0111   | 0100 |
| 8       | 1000   | 1100 |
| 9       | 1001   | 1101 |
| 10      | 1010   | 1111 |
| 11      | 1011   | 1110 |
| 12      | 1100   | 1010 |
| 13      | 1101   | 1011 |
| 14      | 1110   | 1001 |
| 15      | 1111   | 1000 |

### Applications of Gray Code

1. **Shaft Encoders**: Position sensing in robotics
2. **A/D Converters**: Analog to digital conversion
3. **K-Maps**: Simplification of Boolean functions
4. **Error Minimization**: Reduces errors in transitions
5. **Genetic Algorithms**: Mutation operations
6. **Communication**: Minimize errors during state changes

### Why Gray Code?

**Problem with Binary:**
- Multiple bits change: 0111 (7) → 1000 (8)
- During transition, intermediate invalid states possible
- Can cause errors in mechanical systems

**Gray Code Solution:**
- Only one bit changes per transition
- No intermediate invalid states
- Reliable in noisy environments

## Excess-3 Code (XS-3)

### Features
- **Non-weighted code**
- **Self-complementing**: 9's complement obtained by bit inversion
- Formed by adding 3 (0011) to each BCD digit
- Also called Stibitz code

### BCD to Excess-3 Conversion

**Method:**
XS-3 = BCD + 0011

**Excess-3 Table:**

| Decimal | BCD  | +3   | Excess-3 | 9's Complement | XS-3 Complement |
|---------|------|------|----------|----------------|------------------|
| 0       | 0000 | 0011 | 0011     | 9              | 1100             |
| 1       | 0001 | 0011 | 0100     | 8              | 1011             |
| 2       | 0010 | 0011 | 0101     | 7              | 1010             |
| 3       | 0011 | 0011 | 0110     | 6              | 1001             |
| 4       | 0100 | 0011 | 0111     | 5              | 1000             |
| 5       | 0101 | 0011 | 1000     | 4              | 0111             |
| 6       | 0110 | 0011 | 1001     | 3              | 0110             |
| 7       | 0111 | 0011 | 1010     | 2              | 0101             |
| 8       | 1000 | 0011 | 1011     | 1              | 0100             |
| 9       | 1001 | 0011 | 1100     | 0              | 0011             |

### Advantages of Excess-3

1. **Self-Complementing**: Easy to find 9's complement
2. **No Invalid States in Middle**: Better for arithmetic
3. **Simpler Subtraction**: Using complements

### Applications
- Decimal arithmetic units
- Older computer systems
- Calculator circuits

## Other BCD Codes

### 2421 Code
- Weights: 2-4-2-1
- Self-complementing
- Multiple representations possible

### 5211 Code
- Weights: 5-2-1-1
- Self-complementing
- Used in specific applications

## Alphanumeric Codes

### ASCII (American Standard Code for Information Interchange)

**Features:**
- **7-bit code** (128 characters)
- Extended ASCII: 8-bit (256 characters)
- Standard for text representation

**Character Sets:**
- **Control Characters** (0-31): Non-printable
- **Digits** (48-57): '0' to '9'
- **Uppercase** (65-90): 'A' to 'Z'
- **Lowercase** (97-122): 'a' to 'z'
- **Special Characters**: Punctuation, symbols

**Examples:**
- 'A' = 65 = 0100 0001
- 'a' = 97 = 0110 0001  
- '0' = 48 = 0011 0000
- Space = 32 = 0010 0000

### EBCDIC (Extended Binary Coded Decimal Interchange Code)

- **8-bit code**
- Used in IBM mainframes
- 256 characters possible
- Different from ASCII

### Unicode

- **16-bit code** (UTF-16)
- Supports international characters
- Over 1 million characters
- Universal character encoding

## Error Detection Codes

### Parity Bit

**Even Parity:**
- Total 1s (including parity) = even number
- Example: 1011 → 11011 (add 1)

**Odd Parity:**
- Total 1s (including parity) = odd number
- Example: 1011 → 01011 (add 0)

**Limitations:**
- Can detect single-bit errors
- Cannot detect even number of errors
- Cannot correct errors

### Hamming Code

- Can detect and correct single-bit errors
- Detect (not correct) double-bit errors
- Uses multiple parity bits
- Parity bits at positions: 2⁰, 2¹, 2², 2³...

## Key Comparisons

### Binary vs BCD
| Feature | Binary | BCD |
|---------|--------|-----|
| Bits for 99 | 7 bits | 8 bits |
| Conversion | Complex | Easy |
| Arithmetic | Simple | Complex |
| Storage | Efficient | Wasteful |
| Usage | Computers | Display |

### Gray vs Binary
| Feature | Binary | Gray |
|---------|--------|------|
| Bit changes | Multiple | Single |
| Arithmetic | Easy | Difficult |
| Error prone | Yes | No |
| Usage | Computing | Sensing |

## Important Notes

- BCD requires 20% more storage than binary
- Gray code is NOT used for arithmetic
- Excess-3 simplifies decimal subtraction
- ASCII is standard for text files
- Parity can only DETECT errors, not correct
- Choose code based on application requirements

## Applications Summary

- **BCD**: Digital displays, calculators, clocks
- **Gray Code**: Shaft encoders, K-maps, A/D converters
- **Excess-3**: Arithmetic circuits, legacy systems
- **ASCII**: Text files, keyboards, communication
- **Hamming**: Error correction in memory, storage

## Resources

- Reference: Digital Design by M. Morris Mano (Chapter 1)
- Practice code conversions regularly
- Understand trade-offs between different codes
- Study applications to understand usage
