# Boolean Algebra

## Overview
Boolean Algebra is a mathematical system used for analysis and simplification of digital circuits. It deals with binary variables and logic operations.

## Topics Covered

### Fundamental Laws

#### 1. **Idempotent Law**
- a · a = a
- a + a = a

#### 2. **Identity Law**
- a + 0 = a
- a · 1 = a
- a + 1 = 1
- a · 0 = 0

#### 3. **Complement Law**
- a + a' = 1
- a · a' = 0
- 0' = 1
- 1' = 0

#### 4. **Involution Law**
- (a')' = a

#### 5. **Commutative Law**
- a + b = b + a
- a · b = b · a

#### 6. **Associative Law**
- (a + b) + c = a + (b + c)
- (a · b) · c = a · (b · c)

#### 7. **Distributive Law**
- a · (b + c) = a · b + a · c
- a + (b · c) = (a + b) · (a + c)

#### 8. **Absorption Law**
- a + a · b = a
- a · (a + b) = a

#### 9. **De Morgan's Theorem**
- (a + b)' = a' · b'
- (a · b)' = a' + b'

### Boolean Operations

**AND Operation (·)**
- Logical multiplication
- Output is 1 only when all inputs are 1
- Symbol: · or ∧

**OR Operation (+)**
- Logical addition  
- Output is 1 when at least one input is 1
- Symbol: + or ∨

**NOT Operation (')**
- Logical complement/inversion
- Inverts the input
- Symbol: ' or ¯

## Simplification Techniques

### 1. Algebraic Simplification
Apply Boolean laws step by step to reduce expressions

**Example:**
```
F = AB + AB' + A'B
  = A(B + B') + A'B
  = A·1 + A'B
  = A + A'B
  = (A + A')(A + B)
  = 1·(A + B)
  = A + B
```

### 2. Using Karnaugh Maps
Graphical method for simplification (covered in K-Maps section)

### 3. Duality Principle
Change AND ↔ OR and 0 ↔ 1 to get dual expression

## Standard Forms

### Sum of Products (SOP)
- **Canonical SOP**: Each term is a minterm
- **General SOP**: Product terms may not be minterms
- **Minimal SOP**: Simplified SOP form

**Example:** F = AB + AC + BC

### Product of Sums (POS)
- **Canonical POS**: Each term is a maxterm  
- **General POS**: Sum terms may not be maxterms
- **Minimal POS**: Simplified POS form

**Example:** F = (A + B)(A + C)(B + C)

## Minterms and Maxterms

### Minterms
- Product of all variables (complemented or uncomplemented)
- Value = 1 for specific input combination
- Denoted as m₀, m₁, m₂, ...
- Example (3 variables):
  - m₀ = A'B'C' (000)
  - m₇ = ABC (111)

### Maxterms
- Sum of all variables (complemented or uncomplemented)
- Value = 0 for specific input combination
- Denoted as M₀, M₁, M₂, ...
- Example (3 variables):
  - M₀ = A + B + C (000)
  - M₇ = A' + B' + C' (111)

**Relationship:** mᵢ = Mᵢ'

## Important Theorems

### Consensus Theorem
- AB + A'C + BC = AB + A'C
- (A + B)(A' + C)(B + C) = (A + B)(A' + C)

### Transposition Theorem
- AB + A'C = (A + C)(A' + B)

## Practice Problems

1. Simplify: F = ABC + AB'C + A'BC + ABC'
2. Prove: (A + B)(A + C) = A + BC
3. Convert to SOP: F(A,B,C) = ΠM(0,2,5,7)
4. Simplify using De Morgan's: F = ((AB)' + C')'
5. Find complement of: F = AB + A'C

## Applications

- Digital circuit design and analysis
- Logic simplification
- Gate minimization
- Computer arithmetic
- Control systems

## Important Notes

- Always verify simplification by creating truth tables
- Multiple correct simplified forms may exist
- Choose form based on implementation requirements
- SOP is easier for NAND implementation
- POS is easier for NOR implementation

## Circuit Implementation

### From Boolean Expression to Gates
1. Identify operations: AND, OR, NOT
2. Draw gates for each operation
3. Connect according to expression hierarchy
4. Optimize using universal gates if needed

### Gate Conversion
- **NAND gates**: Universal - can implement any Boolean function
- **NOR gates**: Universal - can implement any Boolean function
- NOT = NAND/NOR with inputs tied together
- AND = NAND + NOT
- OR = NOR + NOT

## Resources

- Reference: Digital Design by M. Morris Mano
- Practice Boolean algebra rules regularly
- Use online simulators for gate circuit verification
