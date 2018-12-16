# Rcpp
Summarize something about Rcpp 

## How to make R package with Rcpp and RcppArmadillo
The most simple method to make a R package with Rcpp is to use Rstudio
* Install R packages *Rtools* and *roxygen2*.
* New Project -> New Direcotry -> R package using RcppArmadillo -> Create Project.
* Update DESCRIPTION file. Note: add *RcppParallel* in *LinkingTo* if needed.
* Build -> More -> Configure Build Tools -> Configure -> check all options. (To be updated)
* How to automatically read in data/file when library(package)? (To be updated)

## Bitwise operator in C++/Rcpp
Here are some bitwise operators in C++/Rcpp and some useful examples.
### bitwise operators (work at bit-level)
* **\& (bitwise AND)** Takes two numbers as operands and does AND on every bit of two numbers. The result of AND is 1 only if both bits are 1.
* **\| (bitwise OR)** Takes two numbers as operands and does OR on every bit of two numbers. The result of OR is 1 only if any of the two bits are 1.
* **\^ (bitwise XOR)** Takes two numbers as operands and does XOR on every bit of two numbers. The result of XOR is 1 only if the two bits are different.
* **<< (left shift)** Takes two numbers, left shifts the bits of the first operand, the second operand decides the number of places to shift.
* **>> (right shift)** Takes two numbers, right shifts the bits of the first operand, the second operand decides the number of places to shift.
* **\~ (bitwise NOT)** Takes one number and inverts all bits of it.

### Examples
* Example 1
```cpp
unsigned char* c;
const int pos; // pos = 0b00, 0b01, 0b10, 0b11 (position to insert genotype)
const int geno; // geno = 0b00, 0b01, 0b10, 0b11 (genotype inserted)
(*c) |= (geno << (pos << 1));
```
The above code is 
```cpp
pos1 = pos << 1; // pos1 = 0b000(0d0), 0b010(0d2), 0b100(0d4), 0b110(0d6);
geno1 = geno << pos1; // if pos1 = 0b010(0d2), geno = 0b11, then geno1 = 0b1100;
(*c) = (*c) | geno1; // update (*c) by inserting genotype
```

* Example 2
```cpp
int geno_temp = geno & 3;  // 0d3 = 0b11
geno = geno >> 2;
```

* Example 3
```cpp
unsigned char m_bits_val[8];
int k = 8;
while (k > 0){
  -- k;
  m_bits_val[k] = 1 << k;
}
```

