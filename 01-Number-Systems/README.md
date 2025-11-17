# Number Systems

## Overview
This section covers various number systems used in digital electronics and their conversions.

## Topics Covered

### 1. Decimal Number System
- Base: 10
- Digits: 0-9
- Most commonly used in day-to-day calculations
- Example: 9256₁₀ = 9×10³ + 2×10² + 5×10¹ + 6×10⁰

### 2. Binary Number System
- Base: 2
- Digits: 0, 1
- Fundamental to computer systems
- Example: 1011₂ = 1×2³ + 0×2² + 1×2¹ + 1×2⁰ = 11₁₀

### 3. Octal Number System
- Base: 8
- Digits: 0-7
- Used in earlier computer systems
- 1 octal digit = 3 binary digits
- Example: 367₈ = 3×8² + 6×8¹ + 7×8⁰ = 247₁₀

### 4. Hexadecimal Number System
- Base: 16
- Digits: 0-9, A-F (A=10, B=11, C=12, D=13, E=14, F=15)
- Used in embedded programming
- 1 hex digit = 4 binary digits
- Example: 96A₁₆ = 9×16² + 6×16¹ + 10×16⁰ = 2410₁₀

## Number System Conversions

### Decimal to Binary
**Method**: Division Algorithm
- Repeatedly divide by 2
- Record remainders from bottom to top
- Example: 67₁₀ = 1000011₂

### Binary to Decimal
**Method**: Positional Weight
- Multiply each bit by 2ⁿ where n is position
- Add all results
- Example: 1011₂ = 8 + 0 + 2 + 1 = 11₁₀

### Binary to Octal
- Group binary digits in sets of 3 (from right)
- Convert each group to octal digit
- Example: 110101₂ = 65₈

### Binary to Hexadecimal
- Group binary digits in sets of 4 (from right)
- Convert each group to hex digit
- Example: 11010110₂ = D6₁₆

### Octal to Hexadecimal (via Binary)
- Convert octal to binary (3 bits per digit)
- Convert binary to hex (4 bits per digit)

## Key Formulas

**General Conversion to Decimal:**
```
Number = dₙ×Bⁿ + dₙ₋₁×Bⁿ⁻¹ + ... + d₁×B¹ + d₀×B⁰
```
Where:
- dₙ = digit at position n
- B = base of number system
- n = position (0, 1, 2, ...)

## Important Notes

- When converting decimals with fractional parts, multiply the fraction by the target base repeatedly
- For binary point, bits on right are negative powers of 2
- Always verify your conversions by converting back to original base
- In exams, show all intermediate steps

## Range of Numbers

For an n-bit system:
- **Unsigned**: 0 to 2ⁿ - 1
- **Signed (2's complement)**: -2ⁿ⁻¹ to 2ⁿ⁻¹ - 1

## Applications

- **Binary**: All digital systems, computers
- **Octal**: Unix file permissions, legacy systems
- **Hexadecimal**: Memory addresses, color codes, embedded systems
- **Decimal**: Human-readable representation

## Resources

- Reference: Digital Design by M. Morris Mano
- Practice conversions regularly for mastery
- Use online calculators to verify your answers
