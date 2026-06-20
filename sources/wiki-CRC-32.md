---
source: https://en.wikipedia.org/wiki/CRC-32
fetched: 2026-06-19
---

|  | This articlecontainsinstructions or advice.Wikipedia is not a guidebook; please helprewrite such contentto be encyclopedic or move it toWikiversity,Wikibooks, orWikivoyage.(February 2023) |
| --- | --- |

 
|  | The topic of this articlemay not meet Wikipedia'sgeneral notability guideline.Please help to demonstrate the notability of the topic by citingreliable secondary sourcesthat areindependentof the topic and provide significant coverage of it beyond a mere trivial mention. If notability cannot be shown, the article is likely to bemerged,redirected, ordeleted.Find sources:"Computation of cyclic redundancy checks"–news·newspapers·books·scholar·JSTOR(February 2023)(Learn how and when to remove this message) |
| --- | --- |

 

Computation of a [cyclic redundancy check](./Cyclic_redundancy_check) is derived from the [mathematics](./Mathematics) of [polynomial division, modulo two](./Mathematics_of_cyclic_redundancy_checks). In practice, it resembles [long division](./Long_division) of the [binary](./Binary_code) message string, with a fixed number of zeroes appended, by the "generator polynomial" string except that [exclusive or](./Exclusive_or) operations replace subtractions.  Division of this type is efficiently realised in hardware by a modified [shift register](./Shift_register),[[1]](./Computation_of_cyclic_redundancy_checks#cite_note-1) and in software by a series of equivalent [algorithms](./Algorithm), starting with simple code close to the mathematics and becoming faster (and arguably more [obfuscated](./Obfuscated_code)[[2]](./Computation_of_cyclic_redundancy_checks#cite_note-williams96-2)) through [byte](./Byte)-wise [parallelism](./Parallelism_(computing)) and [space–time tradeoffs](./Space–time_tradeoff).

 [![](//upload.wikimedia.org/wikipedia/commons/0/02/CRC8-gen.gif)](./File:CRC8-gen.gif)Example of generating an 8-bit [CRC](./Cyclic_redundancy_check). The generator is a Galois-type [shift register](./Linear-feedback_shift_register) with [XOR gates](./XOR_gate) placed according to powers (white numbers) of *x* in the generator polynomial. The message stream may be any length. After it has been shifted through the register, followed by 8 zeroes, the result in the register is the checksum. [![](//upload.wikimedia.org/wikipedia/commons/1/17/CRC8-rx.gif)](./File:CRC8-rx.gif)Checking received data with checksum. The received message is shifted through the same register as used in the generator, but the received checksum is attached to it instead of zeroes. Correct data yields the all-zeroes result; a corrupted bit in either the message or checksum would give a different result, warning that an error has occurred. 

Various CRC standards extend the polynomial division algorithm by specifying an initial shift register value, a final Exclusive-Or step and, most critically, a bit ordering ([endianness](./Endianness)).  As a result, the code seen in practice deviates confusingly from "pure" division,[[2]](./Computation_of_cyclic_redundancy_checks#cite_note-williams96-2) and the register may shift left or right.

 

## Example

 For a discussion of polynomial division modulo two, see [Mathematics of cyclic redundancy checks](./Mathematics_of_cyclic_redundancy_checks). 

As an example of implementing polynomial division in hardware, suppose that we are trying to compute an 8-bit CRC of an 8-bit message made of the [ASCII](./ASCII) character "W", which is binary 010101112, decimal 8710, or [hexadecimal](./Hexadecimal) 5716.  For illustration, we will use the CRC-8-ATM ([HEC](./CRC-based_framing)) polynomial      x  8   +  x  2   + x + 1   {\displaystyle x^{8}+x^{2}+x+1}  ![{\displaystyle x^{8}+x^{2}+x+1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9aeac5149ba7d39c70a5adf775f3ccf3c458c285).  Writing the first bit transmitted (the coefficient of the highest power of     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4)) on the left, this corresponds to the 9-bit string "100000111".

 

The byte value 5716 can be transmitted in two different orders, depending on the bit ordering convention used.  Each one generates a different message polynomial     M ( x )   {\displaystyle M(x)}  ![{\displaystyle M(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8d2fab18f2df9b523ef8b7b63a291317294fc708).  Msbit-first, this is      x  6   +  x  4   +  x  2   + x + 1   {\displaystyle x^{6}+x^{4}+x^{2}+x+1}  ![{\displaystyle x^{6}+x^{4}+x^{2}+x+1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/eb383a0c405fdddeb524a540d2d8103739a5e10c) = 01010111, while lsbit-first, it is      x  7   +  x  6   +  x  5   +  x  3   + x   {\displaystyle x^{7}+x^{6}+x^{5}+x^{3}+x}  ![{\displaystyle x^{7}+x^{6}+x^{5}+x^{3}+x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0b5662f60b50443f1374dbb729897bb359c71e62) = 11101010.  These can then be multiplied by      x  8     {\displaystyle x^{8}}  ![{\displaystyle x^{8}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fd38d454ecee1b299d927818db4edee936f3092e) to produce two 16-bit message polynomials      x  8   M ( x )   {\displaystyle x^{8}M(x)}  ![{\displaystyle x^{8}M(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bbd57f2d1425269a4e1279974d3671cb7a837d1e).

 

Computing the remainder then consists of subtracting multiples of the generator polynomial     G ( x )   {\displaystyle G(x)}  ![{\displaystyle G(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1d6d96c680c58289ec8857273d6938cacd742084).  This is just like decimal long division, but even simpler because the only possible multiples at each step are 0 and 1, and the subtractions [borrow](./Carry_(arithmetic)) "from infinity" instead of reducing the upper digits. Because we do not care about the quotient, there is no need to record it.

 
| Most-significant bit first | Least-significant bit first |
| --- | --- |
| 0101011100000000−000000000=0101011100000000−100000111=0001011011000000−000000000=0001011011000000−100000111=0000011010110000−000000000=0000011010110000−100000111=0000001010101100−100000111=0000000010100010−000000000=0000000010100010 |  | 0 | 1 | 0 | 1 | 0 | 1 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | − | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | = | 0 | 1 | 0 | 1 | 0 | 1 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |  | − | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 | = | 0 | 0 | 0 | 1 | 0 | 1 | 1 | 0 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 |  |  | − | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | = | 0 | 0 | 0 | 1 | 0 | 1 | 1 | 0 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 |  |  |  | − | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 | = | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 0 | 1 | 0 | 1 | 1 | 0 | 0 | 0 | 0 |  |  |  |  | − | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | = | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 0 | 1 | 0 | 1 | 1 | 0 | 0 | 0 | 0 |  |  |  |  |  | − | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 | = | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 1 | 0 | 1 | 0 | 1 | 1 | 0 | 0 |  |  |  |  |  |  | − | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 | = | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 1 | 0 | 0 | 0 | 1 | 0 |  |  |  |  |  |  |  | − | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | = | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 1 | 0 | 0 | 0 | 1 | 0 | 1110101000000000−100000111=0110100110000000−100000111=0010100001000000−100000111=0000100010100000−000000000=0000100010100000−100000111=0000000010011000−000000000=0000000010011000−000000000=0000000010011000−000000000=0000000010011000 |  | 1 | 1 | 1 | 0 | 1 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | − | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 | = | 0 | 1 | 1 | 0 | 1 | 0 | 0 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |  | − | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 | = | 0 | 0 | 1 | 0 | 1 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 |  |  | − | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 | = | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 0 | 1 | 0 | 0 | 0 | 0 | 0 |  |  |  | − | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | = | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 0 | 1 | 0 | 0 | 0 | 0 | 0 |  |  |  |  | − | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 | = | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 1 | 1 | 0 | 0 | 0 |  |  |  |  |  | − | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | = | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 1 | 1 | 0 | 0 | 0 |  |  |  |  |  |  | − | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | = | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 1 | 1 | 0 | 0 | 0 |  |  |  |  |  |  |  | − | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | = | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 1 | 1 | 0 | 0 | 0 |
|  | 0 | 1 | 0 | 1 | 0 | 1 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| − | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| = | 0 | 1 | 0 | 1 | 0 | 1 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
|  | − | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 |
| = | 0 | 0 | 0 | 1 | 0 | 1 | 1 | 0 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 |
|  |  | − | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| = | 0 | 0 | 0 | 1 | 0 | 1 | 1 | 0 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 |
|  |  |  | − | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 |
| = | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 0 | 1 | 0 | 1 | 1 | 0 | 0 | 0 | 0 |
|  |  |  |  | − | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| = | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 0 | 1 | 0 | 1 | 1 | 0 | 0 | 0 | 0 |
|  |  |  |  |  | − | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 |
| = | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 1 | 0 | 1 | 0 | 1 | 1 | 0 | 0 |
|  |  |  |  |  |  | − | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 |
| = | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 1 | 0 | 0 | 0 | 1 | 0 |
|  |  |  |  |  |  |  | − | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| = | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 1 | 0 | 0 | 0 | 1 | 0 |
|  | 1 | 1 | 1 | 0 | 1 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| − | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 |
| = | 0 | 1 | 1 | 0 | 1 | 0 | 0 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
|  | − | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 |
| = | 0 | 0 | 1 | 0 | 1 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 |
|  |  | − | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 |
| = | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 0 | 1 | 0 | 0 | 0 | 0 | 0 |
|  |  |  | − | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| = | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 0 | 1 | 0 | 0 | 0 | 0 | 0 |
|  |  |  |  | − | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 |
| = | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 1 | 1 | 0 | 0 | 0 |
|  |  |  |  |  | − | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| = | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 1 | 1 | 0 | 0 | 0 |
|  |  |  |  |  |  | − | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| = | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 1 | 1 | 0 | 0 | 0 |
|  |  |  |  |  |  |  | − | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| = | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 1 | 1 | 0 | 0 | 0 |

 

Observe that after each subtraction, the bits are divided into three groups: at the beginning, a group which is all zero; at the end, a group which is unchanged from the original; and a blue shaded group in the middle which is "interesting". The "interesting" group is 8 bits long, matching the degree of the polynomial. Every step, the appropriate multiple of the polynomial is subtracted to make the zero group one bit longer, and the unchanged group becomes one bit shorter, until only the final remainder is left.

 

In the msbit-first example, the remainder polynomial is      x  7   +  x  5   + x   {\displaystyle x^{7}+x^{5}+x}  ![{\displaystyle x^{7}+x^{5}+x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/69cfc04b8b2ffe16ff445ba51df3cae07139be6d).  Converting to a hexadecimal number using the convention that the highest power of *x* is the msbit; this is A216.  In the lsbit-first, the remainder is      x  7   +  x  4   +  x  3     {\displaystyle x^{7}+x^{4}+x^{3}}  ![{\displaystyle x^{7}+x^{4}+x^{3}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0bf6cdfaee9bb4f051e270c3f4f57062c2ae1fd2).  Converting to hexadecimal using the convention that the highest power of *x* is the lsbit, this is 1916.

 

## Implementation

 

Writing out the full message at each step, as done in the example above, is very tedious.  Efficient implementations
use an     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b)-bit [shift register](./Shift_register) to hold only the interesting bits.  Multiplying the polynomial by     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) is equivalent to shifting the register by one place, as the coefficients do not change in value but only move up to the next term of the polynomial.

 

Here is a first draft of some [pseudocode](./Pseudocode) for computing an *n*-bit CRC.  It uses a contrived [composite data type](./Object_composition) for polynomials, where `x` is not an integer variable, but a [constructor](./Constructor_(computer_science)) generating a *Polynomial* [object](./Object_(computer_science)) that can be added, multiplied and exponentiated.  To `xor` two polynomials is to add them, modulo two; that is, to [exclusive OR](./Exclusive_OR) the coefficients of each matching term from both polynomials.

 
```
function crc(bit array bitString[1..len], int len) {
    remainderPolynomial := polynomialForm(bitString[1..n])   // First n bits of the message
    // A popular variant complements remainderPolynomial here; see § Preset to −1 below
    for i from 1 to len {
        remainderPolynomial := remainderPolynomial * x + bitString[i+n] * x0   // Define bitString[k]=0 for k>len
        if coefficient of xn of remainderPolynomial = 1 {
            remainderPolynomial := remainderPolynomial xor generatorPolynomial
        }
    }
    // A popular variant complements remainderPolynomial here; see § Post-invert below
    return remainderPolynomial
}
```
 **Code fragment 1: Simple polynomial division** 

Note that this example code avoids the need to specify a bit-ordering convention by not using bytes; the input `bitString` is already in the form of a [bit array](./Bit_array), and the `remainderPolynomial` is manipulated in terms of polynomial operations; the multiplication by     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) could be a left or right shift, and the addition of `bitString[i+n]` is done to the      x  0     {\displaystyle x^{0}}  ![{\displaystyle x^{0}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1871ffeb57c11624b375dbb7157d5887c706eb87) coefficient, which could be the right or left end of the register.

 

This code has two disadvantages.  First, it actually requires an *n*+1-bit register to hold the `remainderPolynomial` so that the      x  n     {\displaystyle x^{n}}  ![{\displaystyle x^{n}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/150d38e238991bc4d0689ffc9d2a852547d2658d) coefficient can be tested. More significantly, it requires the `bitString` to be padded with *n* zero bits.

 

The first problem can be solved by testing the      x  n − −  1     {\displaystyle x^{n-1}}  ![{\displaystyle x^{n-1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c427ee189e46907f667b4f32462c6c2aa75c1983) coefficient of the `remainderPolynomial` before it is multiplied by     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4).

 

The second problem could be solved by doing the last *n* iterations differently, but there is a more subtle optimization which is used universally, in both hardware and software implementations.

 

Because the XOR operation used to subtract the generator polynomial from the message is [commutative](./Commutative) and [associative](./Associative), it does not matter in what order the various inputs are combined into the `remainderPolynomial`.  And specifically, a given bit of the `bitString` does not need to be added to the `remainderPolynomial` until the very last instant when it is tested to determine whether to `xor` with the `generatorPolynomial`.

 

This eliminates the need to preload the `remainderPolynomial` with the first *n* bits of the message, as well:

 
```
function crc(bit array bitString[1..len], int len) {
    remainderPolynomial := 0
    // A popular variant complements remainderPolynomial here; see § Preset to −1 below
    for i from 1 to len {
        remainderPolynomial := remainderPolynomial xor (bitstring[i] * xn−1)
        if (coefficient of xn−1 of remainderPolynomial) = 1 {
            remainderPolynomial := (remainderPolynomial * x) xor generatorPolynomial
        } else {
            remainderPolynomial := (remainderPolynomial * x)
        }
    }
    // A popular variant complements remainderPolynomial here; see § Post-invert below
    return remainderPolynomial
}
```
 **Code fragment 2: Polynomial division with deferred message XORing** 

This is the standard bit-at-a-time hardware CRC implementation, and is well worthy of study; once you understand why this computes exactly the same result as the first version, the remaining optimizations are quite straightforward.  If `remainderPolynomial` is only *n* bits long, then the      x  n     {\displaystyle x^{n}}  ![{\displaystyle x^{n}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/150d38e238991bc4d0689ffc9d2a852547d2658d) coefficients of it and of `generatorPolynomial` are simply discarded.  This is the reason that you will usually see CRC polynomials written in binary with the leading coefficient omitted.

 

In software, it is convenient to note that while one *may* delay the `xor` of each bit until the very last moment, it is also possible to do it earlier.  It is usually convenient to perform the `xor` a [byte](./Byte) at a time, even in a bit-at-a-time implementation.  Here, we take the input in 8-bit bytes:

 
```
function crc(byte array string[1..len], int len) {
    remainderPolynomial := 0
    // A popular variant complements remainderPolynomial here; see § Preset to −1 below
    for i from 1 to len {
        remainderPolynomial := remainderPolynomial xor polynomialForm(string[i]) * xn−8
        for j from 1 to 8 {    // Assuming 8 bits per byte
            if coefficient of xn−1 of remainderPolynomial = 1 {
                remainderPolynomial := (remainderPolynomial * x) xor generatorPolynomial
            } else {
                remainderPolynomial := (remainderPolynomial * x)
            }
        }
    }
    // A popular variant complements remainderPolynomial here; see § Post-invert below
    return remainderPolynomial
}
```
 **Code fragment 3: Polynomial division with bytewise message XORing** 

This is usually the most compact software implementation, used in [microcontrollers](./Microcontrollers) when space is at a premium over speed.

 

## Bit ordering (endianness)

 

When implemented in [bit serial](./Bit-serial_architecture) [hardware](./Hardware_(computer)), the generator polynomial uniquely describes the bit assignment; the first bit transmitted is always the coefficient of the highest power of     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4), and the last     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) bits transmitted are the CRC remainder     R ( x )   {\displaystyle R(x)}  ![{\displaystyle R(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cd5e851b43895fbe06436240dc7daa4d2033f082), starting with the coefficient of      x  n − −  1     {\displaystyle x^{n-1}}  ![{\displaystyle x^{n-1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c427ee189e46907f667b4f32462c6c2aa75c1983) and ending with the coefficient of      x  0     {\displaystyle x^{0}}  ![{\displaystyle x^{0}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1871ffeb57c11624b375dbb7157d5887c706eb87), a.k.a. the coefficient of 1.

 

However, when bits are processed a [byte](./Byte) at a time, such as when using [parallel transmission](./Parallel_transmission), byte framing as in [8B/10B encoding](./8B/10B_encoding) or [RS-232](./RS-232)-style [asynchronous serial communication](./Asynchronous_serial_communication), or when implementing a CRC in [software](./Software), it is necessary to specify the bit ordering (endianness) of the data; which bit in each byte is considered "first" and will be the coefficient of the higher power of     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4).

 

If the data is destined for [serial communication](./Serial_communication), it is best to use the bit ordering the data will ultimately be sent in.  This is because a CRC's ability to detect [burst errors](./Burst_error) is based on proximity in the message polynomial     M ( x )   {\displaystyle M(x)}  ![{\displaystyle M(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8d2fab18f2df9b523ef8b7b63a291317294fc708); if adjacent polynomial terms are not transmitted sequentially, a physical error burst of one length may be seen as a longer burst due to the rearrangement of bits.

 

For example, both [IEEE 802](./IEEE_802) ([ethernet](./Ethernet)) and [RS-232](./RS-232) ([serial port](./Serial_port)) standards specify least-significant bit first (little-endian) transmission, so a software CRC implementation to protect data sent across such a link should map the least significant bits in each byte to coefficients of the highest powers of     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4).  On the other hand, [floppy disks](./Floppy_disk) and most [hard drives](./Hard_drive) write the most significant bit of each byte first.

 

The lsbit-first CRC is slightly simpler to implement in software, so is somewhat more commonly seen, but many programmers find the msbit-first bit ordering easier to follow.  Thus, for example, the [XMODEM](./XMODEM)-CRC extension, an early use of CRCs in software, uses an msbit-first CRC.

 

So far, the pseudocode has avoided specifying the ordering of bits within bytes by describing shifts in the pseudocode as multiplications by     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) and writing explicit conversions from binary to polynomial form.  In practice, the CRC is held in a standard binary register using a particular bit-ordering convention.  In msbit-first form, the most significant binary bits will be sent first and so contain the higher-order polynomial coefficients, while in lsbit-first form, the least-significant binary bits contain the higher-order coefficients.  The above pseudocode can be written in both forms.  For concreteness, this uses the 16-bit  CRC-16-[CCITT](./CCITT) polynomial      x  16   +  x  12   +  x  5   + 1   {\displaystyle x^{16}+x^{12}+x^{5}+1}  ![{\displaystyle x^{16}+x^{12}+x^{5}+1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/661d89787e958d98fb6da5c0c2185fc92a176514):

 
```
// Most significant bit first (big-endian)
// (x16)+x12+x5+1 = (1) 0001 0000 0010 0001 = 0x1021
function crc(byte array string[1..len], int len) {
    rem := 0
    // A popular variant complements rem here
    for i from 1 to len {
        rem  := rem xor (string[i] leftShift (n-8))   // n = 16 in this example
        for j from 1 to 8 {       // Assuming 8 bits per byte
            if rem and 0x8000 {   // Test x15 coefficient
                rem  := (rem leftShift 1) xor 0x1021
            } else {
                rem  := rem leftShift 1
            }
            rem  := rem and 0xffff      // Trim remainder to 16 bits
        }
    }
    // A popular variant complements rem here
    return rem
}
```
 **Code fragment 4: Shift register based division, MSB first** 
```
// Least significant bit first (little-endian)
// 1+x5+x12+(x16) = 1000 0100 0000 1000 (1) = 0x8408
function crc(byte array string[1..len], int len) {
    rem  := 0
    // A popular variant complements rem here
    for i from 1 to len {
        rem  := rem xor string[i]
        for j from 1 to 8 {       // Assuming 8 bits per byte
            if rem and 0x0001 {   // Test x15 coefficient
                rem  := (rem rightShift 1) xor 0x8408
            } else {
                rem  := rem rightShift 1
            }
        }
    }
    // A popular variant complements rem here
    return rem
}
```
 **Code fragment 5: Shift register based division, LSB first** 

Note that the lsbit-first form avoids the need to shift `string[i]` before the `xor`.  In either case, be sure to transmit the bytes of the CRC in the order that matches your chosen bit-ordering convention.

 

## Multi-bit computation using lookup tables

 

Faster software implementations process more than one bit of dividend per iteration using [lookup tables](./Lookup_table), indexed by highest order coefficients of `rem`, to [memoize](./Memoize) the per-bit division steps.

 

### Sarwate algorithm (single lookup table)

 

The most common technique uses a 256-entry lookup table, to process 8 bits of input per iteration.[[3]](./Computation_of_cyclic_redundancy_checks#cite_note-3)  This replaces the body of the outer loop (over `i`) with:

 
```
// Msbit-first
rem = (rem leftShift 8) xor big_endian_table[string[i] xor ((leftmost 8 bits of rem) rightShift (n-8))]
// Lsbit-first
rem = (rem rightShift 8) xor little_endian_table[string[i] xor (rightmost 8 bits of rem)]
```
 **Code fragment 6: Cores of table based division** 

Using a 256-entry table is usually most convenient, but other sizes can be used.  In small microcontrollers, using a 16-entry table to process four bits at a time gives a useful speed improvement while keeping the table small.  On computers with ample storage, a 65536-entry table can be used to process 16 bits at a time.

 

#### Generating the lookup table

 

The software to generate the lookup table is so small and fast that it is usually faster to compute them on program startup than to load precomputed tables from storage.  One popular technique is to use the bit-at-a-time code 256 times to generate the CRCs of the 256 possible 8-bit bytes.[[4]](./Computation_of_cyclic_redundancy_checks#cite_note-PNGspec-4)  However, this can be optimized significantly by taking advantage of the property that `table[i xor j] == table[i] xor table[j]`.  Only the table entries corresponding to powers of two need to be computed directly.

 

In the following example code, `crc` holds the value of `table[i]`:

 
```
big_endian_table[0] := 0
crc := 0x8000 // Assuming a 16-bit polynomial
i := 1
do {
    if crc and 0x8000 {
        crc := (crc leftShift 1) xor 0x1021 // The CRC polynomial
    } else {
        crc := crc leftShift 1
    }
    // crc is the value of big_endian_table[i]; let j iterate over the already-initialized entries
    for j from 0 to i−1 {
        big_endian_table[i + j] := crc xor big_endian_table[j];
    }
    i := i leftshift 1
} while i < 256
```
 **Code fragment 7: Byte-at-a-time CRC table generation, msbit-first** 
```
little_endian_table[0] := 0
crc := 1;
i := 128
do {
    if crc and 1 {
        crc := (crc rightShift 1) xor 0x8408 // The CRC polynomial
    } else {
        crc := crc rightShift 1
    }
    // crc is the value of little_endian_table[i]; let j iterate over the already-initialized entries
    for j from 0 to 255 by 2 × i {
        little_endian_table[i + j] := crc xor little_endian_table[j];
    }
    i := i rightshift 1
} while i > 0
```
 **Code fragment 8: Byte-at-a-time CRC table generation, lsbit-first** 

In these code samples, the table index `i + j` is equivalent to `i xor j`; you may use whichever form is more convenient.

 

#### CRC-32 example

 

One of the most commonly encountered CRC polynomials is known as **CRC-32**, used by (among others) [Ethernet](./Ethernet), [FDDI](./FDDI), [ZIP](./ZIP_(file_format)) and other [archive formats](./Archive_formats), and [PNG](./Portable_Network_Graphics) [image format](./Image_format).  Its polynomial can be written msbit-first as 0x04C11DB7, or lsbit-first as 0xEDB88320.

 

This is a practical example for the CRC-32 variant of CRC.[[5]](./Computation_of_cyclic_redundancy_checks#cite_note-5)

 

An alternate source is the W3C webpage on PNG, which includes an appendix with a short and simple table-driven implementation in C of CRC-32.[[4]](./Computation_of_cyclic_redundancy_checks#cite_note-PNGspec-4) You will note that the code corresponds to the lsbit-first byte-at-a-time algorithm presented here, and the table is generated using the bit-at-a-time code.

 
```
Function CRC32
   Input:
      data:  Bytes     // Array of bytes
   Output:
      crc32: UInt32    // 32-bit unsigned CRC-32 value
// Initialize CRC-32 to starting value
crc32 ← 0xFFFFFFFF
for each byte in data do
   nLookupIndex ← (crc32 xor byte) and 0xFF
   crc32 ← (crc32 shr 8) xor CRCTable[nLookupIndex]  // CRCTable is an array of 256 32-bit constants
// Finalize the CRC-32 value by inverting all the bits
crc32 ← crc32 xor 0xFFFFFFFF
return crc32
```
 

In C, the algorithm looks like:

 
```
#include <stdint.h> // uint32_t, uint8_t
#include <stddef.h> // size_t

static uint32_t CRCTable[256];

// Initialization by multiple threads is redundant, but safe.
static void CRC32_init(void)
{
	uint32_t crc32 = 1;
    // C guarantees CRCTable[0] = 0 already.
	for (unsigned int i = 128; i; i >>= 1) {
		crc32 = (crc32 >> 1) ^ (crc32 & 1 ? 0xedb88320 : 0);
		for (unsigned int j = 0; j < 256; j += 2*i)
        	CRCTable[i + j] = crc32 ^ CRCTable[j];
	}
}

uint32_t CRC32(const uint8_t data[], size_t data_length)
{
	uint32_t crc32 = 0xFFFFFFFFu;

	if (CRCTable[255] == 0)
		CRC32_init();
	
	for (size_t i = 0; i < data_length; i++) {
		crc32 ^= data[i];
		crc32 = (crc32 >> 8) ^ CRCTable[crc32 & 0xFF];
	}
	
	// Finalize the CRC-32 value by inverting all the bits
	crc32 ^= 0xFFFFFFFFu;
	return crc32;
}

```
 

### Byte-slicing using multiple tables

 

There exists a slice-by-*n* (typically slice-by-8 for CRC32) algorithm that usually doubles or triples the performance compared to the Sarwate algorithm. Instead of reading 8 bits at a time, the algorithm reads 8*n* bits at a time. Doing so maximizes performance on [superscalar](./Superscalar) processors.[[6]](./Computation_of_cyclic_redundancy_checks#cite_note-6)[[7]](./Computation_of_cyclic_redundancy_checks#cite_note-7)[[8]](./Computation_of_cyclic_redundancy_checks#cite_note-8)[[9]](./Computation_of_cyclic_redundancy_checks#cite_note-9)

 

It is unclear who actually invented the algorithm.[[10]](./Computation_of_cyclic_redundancy_checks#cite_note-10)

 

To understand the advantages, start with the slice-by-2 case.  We wish to compute a CRC two bytes (16 bits) at a time, but the standard table-based approach would require an inconveniently large 65536-entry table.  As mentioned in [§ Generating the lookup table](./Computation_of_cyclic_redundancy_checks#Generating_the_lookup_table), CRC tables have the property that `table[i xor j] = table[i] xor table[j]`.  We can use this identity to replace the large table by two 256-entry tables: `table[i + 256 × j] = table_low[i] xor table_high[j]`.

 

So the large table is not stored explicitly, but each iteration computes the CRC value that would be there by combining the values in two smaller tables.  That is, the 16-bit index is "sliced" into two 8-bit indexes.  At first glance, this seems pointless; why do two lookups in separate tables, when the standard byte-at-a-time algorithm would do two lookups in the *same* table?

 

The difference is [instruction-level parallelism](./Instruction-level_parallelism).  In the standard algorithm, the index for each lookup depends on the value fetched in the previous one.  Thus, the second lookup cannot begin until the first lookup is complete.

 

When sliced tables are used, both lookups can begin at the same time.  If the processor can perform two loads in parallel (2020s microprocessors can keep track of over 100 loads in progress), then this has the potential to double the speed of the inner loop.

 

This technique can obviously be extended to as many slices as the processor can benefit from.

 

When the slicing width *equals* the CRC size, there is a minor speedup.  In the part of the basic Sarwate algorithm where the previous CRC value is shifted by the size of the table lookup, the previous CRC value is shifted away entirely (what remains is all zero), so the XOR can be eliminated from the critical path.

 

The resultant slice-by-*n* inner loop consists of:

 
1. XOR the current CRC with the next *n* bytes of the message,
2. look up each byte of the resultant value in the *n* slice tables, then
3. XOR the *n* results to get the next CRC.

 

This still has the property that all of the loads in the second step must be completed before the next iteration can commence, resulting in regular pauses during which the processor's memory subsystem (in particular, the data cache) is unused.  However, when the slicing width *exceeds* the CRC size, a significant second speedup appears.

 

This is because a portion of the results of the first step *no longer depend* on any previous iteration.  When XORing a 32-bit CRC with 64 bits of message, half of the result is simply a copy of the message.  If coded carefully (to avoid creating a false [data dependency](./Data_dependency)), half of the slice table loads can begin *before* the previous loop iteration has completed.  The result is enough work to keep the processor's memory subsystem *continuously* busy, which achieves maximum performance.  As mentioned, on post-2000 microprocessors, slice-by-8 is generally sufficient to reach this level.

 

There is no particular need for the slices to be 8 bits wide.  For example, it would be entirely possible to compute a CRC 64 bits at a time using a slice-by-9 algorithm, using 9 128-entry lookup tables to handle 63 bits, and the 64th bit handled by the bit-at-a-time algorithm (which is effectively a 1-bit, 2-entry lookup table).  This would almost halve the table size (going from 8×256 = 2048 entries to 9×128 = 1152) at the expense of one more data-dependent load per iteration.

 

## Multi-bit computation without lookup tables

 

Parallel update for a byte or a word at a time can also be done explicitly, without a table.[[11]](./Computation_of_cyclic_redundancy_checks#cite_note-11) For each bit an equation is solved after 8 bits have been shifted in.

 

Multiple reduction steps are normally expressed as a matrix operation.  One shift and reduction modulo a degree-    n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) generator polynomial     G ( x )   {\displaystyle G(x)}  ![{\displaystyle G(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1d6d96c680c58289ec8857273d6938cacd742084) is equivalent to multiplication by the     n × ×  n   {\displaystyle n\times n}  ![{\displaystyle n\times n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/59d2b4cb72e304526cf5b5887147729ea259da78) [companion matrix](./Companion_matrix)     A = C ( G )   {\displaystyle A=C(G)}  ![{\displaystyle A=C(G)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/14f676293742ed30320c82d76e3f8b35cdc24b16).      r   {\displaystyle r}  ![{\displaystyle r}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0d1ecb613aa2984f0576f70f86650b7c2a132538) steps are written as the matrix      A  r   = C ( G  )  r     {\displaystyle A^{r}=C(G)^{r}}  ![{\displaystyle A^{r}=C(G)^{r}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d907ad206efd668ad3332b57c5ec33b898e2bd68).

 

This technique is normally used in high-speed hardware implementations, but is practical in software for small or sparse CRC polynomials.[[12]](./Computation_of_cyclic_redundancy_checks#cite_note-12)  For large, dense CRC polynomials, the code becomes impractically long.

 

### Examples for sparse polynomials

 

The following tables list the equations processing 8 bits at a time modulo some commonly used polynomials, using the following symbols:

 
| ci | CRC bit 7…0 (or 15…0) before update |
| --- | --- |
| ri | CRC bit 7…0 (or 15…0) after update |
| di | input data bit 7…0 |
| ei= di+ ci | ep= e7+ e6+ … + e1+ e0(parity bit) |
| si= di+ ci+8 | sp= s7+ s6+ … + s1+ s0(parity bit) |

 
| Polynomial: | x(x7+x3+ 1)(left-shifted CRC-7-CCITT) | x8+x5+x4+ 1(CRC-8-Dallas/Maxim) |
| --- | --- | --- |
| Coefficients: | 0x12 = (0x09 << 1)(msbit-first) | 0x8c(lsbit-first) |
| r0←r1←r2←r3←r4←r5←r6←r7← | 0
e0+ e4+ e7e1+ e5e2+ e6e3+ e7+ e0+ e4+ e7e4+ e1+ e5e5+ e2+ e6e6+ e3+ e7 | e0+ e4+ e1+ e0+ e5+ e2+ e1e1+ e5+ e2+ e1+ e6+ e3+ e2+ e0e2+ e6+ e3+ e2+ e0+ e7+ e4+ e3+ e1e3+ e0+ e7+ e4+ e3+ e1e4+ e1+ e0e5+ e2+ e1e6+ e3+ e2+ e0e7+ e4+ e3+ e1 |
| C codefragments: | uint8_tc,d,e,f,r;…e=c^d;f=e^(e>>4)^(e>>7);r=(f<<1)^(f<<4); | uint8_tc,d,e,f,r;…e=c^d;f=e^(e<<3)^(e<<4)^(e<<6);r=f^(f>>4)^(f>>5); |

 
| Polynomial: | x16+x12+x5+ 1(CRC-16-CCITT) |
| --- | --- |
| Coefficients: | 0x1021(msbit-first) | 0x8408(lsbit-first) |
| r0←r1←r2←r3←r4←r5←r6←r7←r8←r9←r10←r11←r12←r13←r14←r15← | s4+ s0s5+ s1s6+ s2s7+ s3s4s5+ s4+ s0s6+ s5+ s1s7+ s6+ s2c0+ s7+ s3c1+ s4c2+ s5c3+ s6c4+ s7+ s4+ s0c5+ s5+ s1c6+ s6+ s2c7+ s7+ s3 | c8+ e4+ e0c9+ e5+ e1c10+ e6+ e2c11+ e0+ e7+ e3c12+ e1c13+ e2c14+ e3c15+ e4+ e0e0+ e5+ e1e1+ e6+ e2e2+ e7+ e3e3e4+ e0e5+ e1e6+ e2e7+ e3 |
| C codefragments: | uint8_td,s,t;uint16_tc,r;…s=d^(c>>8);t=s^(s>>4);r=(c<<8)^t^(t<<5)^(t<<12); | uint8_td,e,f;uint16_tc,r;…e=c^d;f=e^(e<<4);r=(c>>8)^(f<<8)^(f<<3)^(f>>4); |

 
| Polynomial: | x16+x15+x2+ 1(CRC-16-ANSI) |
| --- | --- |
| Coefficients: | 0x8005(MSBF/normal) | 0xa001(LSBF/reverse) |
| r0←r1←r2←r3←r4←r5←r6←r7←r8←r9←r10←r11←r12←r13←r14←r15← | sps0+ sps1+ s0s2+ s1s3+ s2s4+ s3s5+ s4s6+ s5c0+ s7+ s6c1+ s7c2c3c4c5c6c7+ sp | c8+ epc9c10c11c12c13c14+ e0c15+ e1+ e0e2+ e1e3+ e2e4+ e3e5+ e4e6+ e5e7+ e6ep+ e7ep |
| C codefragments: | uint8_td,s,p;uint16_tc,r,t;…s=d^(c>>8);p=s^(s>>4);p=p^(p>>2);p=p^(p>>1);p=p&1;t=p|(s<<1);r=(c<<8)^(t<<15)^t^(t<<1); | uint8_td,e,p;uint16_tc,r,f;…e=c^d;p=e^(e>>4);p=p^(p>>2);p=p^(p>>1);p=p&1;f=e|(p<<8);r=(c>>8)^(f<<6)^(f<<7)^(f>>8); |

 

### Two-step computation

 

For dense polynomials, such as the CRC-32 polynomial, computing the remainder a byte at a time produces equations where each bit depends on up to 8 bits of the previous iteration.  In byte-parallel hardware implementations this calls for either 8-input or cascaded XOR gates which have substantial [gate delay](./Gate_delay).

 

To maximise computation speed, an *intermediate remainder* can be calculated by first computing the CRC of the message modulo a sparse polynomial which is a multiple of the CRC polynomial.  For CRC-32, the polynomial *x*123 + *x*111 + *x*92 + *x*84 + *x*64 + *x*46 + *x*23 + 1 has the property that its terms (feedback taps) are at least 8 positions apart.  Thus, a 123-bit shift register can be advanced 8 bits per iteration using only two-input XOR gates, the fastest possible.  Finally the intermediate remainder can be reduced modulo the standard polynomial in a second slower shift register (once per CRC, rather than once per input byte) to yield the CRC-32 remainder.[[13]](./Computation_of_cyclic_redundancy_checks#cite_note-glaise-13)

 

If 3- or 4-input XOR gates are permitted, shorter intermediate polynomials of degree 71 or 53, respectively, can be used.

 

### State-space transformation

 

The preceding technique works, but requires a large intermediate shift register.  A more hardware-efficient technique which has been used for high-speed networking since c. 2000 is *state-space transformation*.  The inner loop of a     r   {\displaystyle r}  ![{\displaystyle r}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0d1ecb613aa2984f0576f70f86650b7c2a132538)-bit-at-a-time CRC engine is to repeatedly update the intermediate remainder     y   {\displaystyle y}  ![{\displaystyle y}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b8a6208ec717213d4317e666f1ae872e00620a0d) to reflect an     r   {\displaystyle r}  ![{\displaystyle r}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0d1ecb613aa2984f0576f70f86650b7c2a132538)-bit portion of the message      y  i     {\displaystyle y_{i}}  ![{\displaystyle y_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/67d30d30b6c2dbe4d6f150d699de040937ecc95f) using:

      y  i   =  A  r   ⋅ ⋅  (  y  i − −  1   ⊕ ⊕   x  i   ) .   {\displaystyle y_{i}=A^{r}\cdot (y_{i-1}\oplus x_{i}).}  ![{\displaystyle y_{i}=A^{r}\cdot (y_{i-1}\oplus x_{i}).}](https://wikimedia.org/api/rest_v1/media/math/render/svg/446fdb788bb5141c3f9f5899999f2c513d1b679d) 

The implementation challenge is that the [matrix multiplication](./Matrix_multiplication) by      A  r     {\displaystyle A^{r}}  ![{\displaystyle A^{r}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/67a371488ba516131bc48150c958b072556277a2) must be performed in     r   {\displaystyle r}  ![{\displaystyle r}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0d1ecb613aa2984f0576f70f86650b7c2a132538) bit times.  In general, as     r   {\displaystyle r}  ![{\displaystyle r}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0d1ecb613aa2984f0576f70f86650b7c2a132538) increases, the so does the complexity of this multiplication, resulting in a maximum speedup of about     r  /  2.   {\displaystyle r/2.}  ![{\displaystyle r/2.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/53315dda8fd12541bf6cf4b784ac79153907e7ca)[[14]](./Computation_of_cyclic_redundancy_checks#cite_note-14)  To improve on this, first break this up the equation using [distributivity](./Distributivity) into:

      y  i   =  A  r    y  i − −  1   ⊕ ⊕   A  r    x  i   .   {\displaystyle y_{i}=A^{r}y_{i-1}\oplus A^{r}x_{i}.}  ![{\displaystyle y_{i}=A^{r}y_{i-1}\oplus A^{r}x_{i}.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a197cb915713a3f7ef80469197c00a564980b841) 

Then, we find an [invertible matrix](./Invertible_matrix)     T   {\displaystyle T}  ![{\displaystyle T}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ec7200acd984a1d3a3d7dc455e262fbe54f7f6e0) and perform a [change of basis](./Change_of_basis), multipling the intermediate state by      T  − −  1     {\displaystyle T^{-1}}  ![{\displaystyle T^{-1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1a1a5bed0ce2d8adc7fdad412c34ef905fb5026f).  So the iteration becomes:

      T  − −  1    y  i   =  T  − −  1    A  r   T (  T  − −  1    y  i − −  1   ) ⊕ ⊕   T  − −  1    A  r    x  i   .   {\displaystyle T^{-1}y_{i}=T^{-1}A^{r}T(T^{-1}y_{i-1})\oplus T^{-1}A^{r}x_{i}.}  ![{\displaystyle T^{-1}y_{i}=T^{-1}A^{r}T(T^{-1}y_{i-1})\oplus T^{-1}A^{r}x_{i}.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f85bbc827f68827bd27553f65ece7e6b25a4c7a2) 

The final CRC is recovered as     y = T (  T  − −  1   y ) .   {\displaystyle y=T(T^{-1}y).}  ![{\displaystyle y=T(T^{-1}y).}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7d5af37a4b7915f5d7daeaeea3dfb0ac996a91a2)
It's important to note that the input multiplication by      T  − −  1    A  r     {\displaystyle T^{-1}A^{r}}  ![{\displaystyle T^{-1}A^{r}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f37d61e32520321d739a75593afb4b9393ceadcc) and the output multiplication by     T   {\displaystyle T}  ![{\displaystyle T}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ec7200acd984a1d3a3d7dc455e262fbe54f7f6e0) are not time-critical, as they can be [pipelined](./Pipeline_(computing)) to whatever depth is required to meet the performance target.  Only the central multiplication by      T  − −  1    A  r   T   {\displaystyle T^{-1}A^{r}T}  ![{\displaystyle T^{-1}A^{r}T}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ecd20e430ad060c60bb160319db70155a356232d) must be completed within     r   {\displaystyle r}  ![{\displaystyle r}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0d1ecb613aa2984f0576f70f86650b7c2a132538) bit times.  It is possible to find a transformation matrix     T   {\displaystyle T}  ![{\displaystyle T}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ec7200acd984a1d3a3d7dc455e262fbe54f7f6e0) which gives that the form of a companion matrix.  In other words, it can be implemented using the same (fast) 2-input XOR gates as the bit-at-a-time algorithm.[[15]](./Computation_of_cyclic_redundancy_checks#cite_note-15)[[16]](./Computation_of_cyclic_redundancy_checks#cite_note-Kennedy2009-16)  This allows an     r   {\displaystyle r}  ![{\displaystyle r}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0d1ecb613aa2984f0576f70f86650b7c2a132538)-bit parallel CRC to operate     r   {\displaystyle r}  ![{\displaystyle r}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0d1ecb613aa2984f0576f70f86650b7c2a132538) times as fast as a 1-bit serial implementation.

 

There are many possible     n × ×  n   {\displaystyle n\times n}  ![{\displaystyle n\times n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/59d2b4cb72e304526cf5b5887147729ea259da78) transformation matrices with this property, so it is possible to choose one which also minimizes the complexity of the input and output matrices      T  − −  1    A  r     {\displaystyle T^{-1}A^{r}}  ![{\displaystyle T^{-1}A^{r}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f37d61e32520321d739a75593afb4b9393ceadcc) and     T   {\displaystyle T}  ![{\displaystyle T}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ec7200acd984a1d3a3d7dc455e262fbe54f7f6e0).[[16]](./Computation_of_cyclic_redundancy_checks#cite_note-Kennedy2009-16)

 

### Block-wise computation

 
|  | This sectionmay beconfusing or unclearto readers. In particular, the explanation isn't detailed enough to understand without the referenced source, and it's buried behind a paywall, leaving the reader stranded..Please helpclarify the section. There might be a discussion about this onthe talk page.(January 2025)(Learn how and when to remove this message) |
| --- | --- |

 

Block-wise computation of the remainder can be performed in hardware for any CRC polynomial by factorizing the state space [transformation matrix](./Transformation_matrix) needed to compute the remainder into two simpler [Toeplitz matrices](./Toeplitz_matrices).[[17]](./Computation_of_cyclic_redundancy_checks#cite_note-17)

 

## One-pass checking

 

When appending a CRC to a message, it is possible to detach the transmitted CRC, recompute it, and verify the recomputed value against the transmitted one.  However, a simpler technique is commonly
used in hardware.

 

When the CRC is transmitted with the correct byte order (matching the chosen bit-ordering convention), a receiver can compute an overall CRC, over the message *and* the CRC, and if they are correct, the result will be zero.[[18]](./Computation_of_cyclic_redundancy_checks#cite_note-Kadatch2010-18)
This possibility is the reason that most network protocols which include a CRC do so *before* the ending [delimiter](./Delimiter); it is not necessary to know whether the end of the packet is imminent to check the CRC.

 

In fact, a few protocols use the CRC *as* the message delimiter, a technique called [CRC-based framing](./CRC-based_framing).  (This requires multiple frames to detect acquisition or loss of framing, so is limited to applications where the frames are a known length, and the frame contents are sufficiently random that valid CRCs in misaligned data are rare.)

 

## CRC variants

 

In practice, most standards specify presetting the register to all-ones and inverting the CRC before transmission.  This has no effect on the ability of a CRC to detect changed bits, but gives it the ability to notice bits that are added to the message.

 

### Preset to −1

 

The basic mathematics of a CRC accepts (considers as correctly transmitted) messages which, when interpreted as a polynomial, are a multiple of the CRC polynomial.  If some leading 0 bits are prepended to such a message, they will not change its interpretation as a polynomial.  This is equivalent to the fact that 0001 and 1 are the same number.

 

But if the message being transmitted does care about leading 0 bits, the inability of the basic CRC algorithm to detect such a change is undesirable.  If it is possible that a transmission error could add such bits, a simple solution is to start with the `rem` shift register set to some non-zero value; for convenience, the all-ones value is typically used.  This is mathematically equivalent to complementing (binary NOT) the first *n* bits of the message, where *n* is the number of bits in the CRC register.

 

This does not affect CRC generation and checking in any way, as long as both generator and checker use the same initial value.  Any non-zero initial value will do, and a few standards specify unusual values,[[19]](./Computation_of_cyclic_redundancy_checks#cite_note-19) but the all-ones value (−1 in twos complement binary) is by far the most common.  Note that a one-pass CRC generate/check will still produce a result of zero when the message is correct, regardless of the preset value.

 

### Post-invert

 

The same sort of error can occur at the end of a message, albeit with a more limited set of messages.  Appending 0 bits to a message is equivalent to multiplying its polynomial by *x*, and if it was previously a multiple of the CRC polynomial, the result of that multiplication will be, as well.  This is equivalent to the fact that, since 726 is a multiple of 11, so is 7260.

 

A similar solution can be applied at the end of the message, inverting the CRC register before it is appended to the message.  Again, any non-zero change will do; inverting all the bits (XORing with an all-ones pattern) is simply the most common.

 

This has an effect on one-pass CRC checking: instead of producing a result of zero when the message is correct, it produces a fixed non-zero result.  (To be precise, the result is the CRC, with zero preset but with post-invert, of the inversion pattern.)  Once this constant has been obtained (e.g. by performing a one-pass CRC generate/check on an arbitrary message), it can be used directly to verify the correctness of any other message checked using the same CRC algorithm.

 

## See also

 

General category

 
- [Error correction code](./Error_correction_code)
- [List of hash functions](./List_of_hash_functions)
- [Parity](./Parity_(telecommunication)) is equivalent to a 1-bit CRC with polynomial *x*+1.

 

Non-CRC checksums

 
- [Adler-32](./Adler-32)
- [Fletcher's checksum](./Fletcher's_checksum)

 

## References

 
1. [↑](./Computation_of_cyclic_redundancy_checks#cite_ref-1) Dubrova, Elena; Mansouri, Shohreh Sharif (May 2012). ["A BDD-Based Approach to Constructing LFSRS for Parallel CRC Encoding"](http://doi.ieeecomputersociety.org/10.1109/ISMVL.2012.20). *2012 IEEE 42nd International Symposium on Multiple-Valued Logic*. pp. 128–133. [doi](./Doi_(identifier)):[10.1109/ISMVL.2012.20](https://doi.org/10.1109%2FISMVL.2012.20). [ISBN](./ISBN_(identifier)) [978-0-7695-4673-5](./Special:BookSources/978-0-7695-4673-5). [S2CID](./S2CID_(identifier)) [27306826](https://api.semanticscholar.org/CorpusID:27306826).
2. [1](./Computation_of_cyclic_redundancy_checks#cite_ref-williams96_2-0) [2](./Computation_of_cyclic_redundancy_checks#cite_ref-williams96_2-1) Williams, Ross N. (1996-09-24). ["A Painless Guide to CRC Error Detection Algorithms V3.00"](https://web.archive.org/web/20060927004051/http://www.repairfaq.org/filipg/LINK/F_crc_v3.html). Archived from [the original](http://www.repairfaq.org/filipg/LINK/F_crc_v3.html) on 2006-09-27. Retrieved 2016-02-16.
3. [↑](./Computation_of_cyclic_redundancy_checks#cite_ref-3) Sarwate, Dilip V. (August 1998). ["Computation of Cyclic Redundancy Checks via Table Look-Up"](https://doi.org/10.1145%2F63030.63037). *[Communications of the ACM](./Communications_of_the_ACM)*. **31** (8): 1008–1013. [doi](./Doi_(identifier)):[10.1145/63030.63037](https://doi.org/10.1145%2F63030.63037). [S2CID](./S2CID_(identifier)) [5363350](https://api.semanticscholar.org/CorpusID:5363350).
4. [1](./Computation_of_cyclic_redundancy_checks#cite_ref-PNGspec_4-0) [2](./Computation_of_cyclic_redundancy_checks#cite_ref-PNGspec_4-1) ["Portable Network Graphics (PNG) Specification (Second Edition): Annex D, Sample Cyclic Redundancy Code implementation"](https://www.w3.org/TR/PNG/#D-CRCAppendix). [W3C](./W3C). 2003-11-10. Retrieved 2016-02-16.
5. [↑](./Computation_of_cyclic_redundancy_checks#cite_ref-5) ["[MS-ABS]: 32-Bit CRC Algorithm"](https://msdn.microsoft.com/en-us/library/dd905031.aspx). *msdn.microsoft.com*. [Archived](https://web.archive.org/web/20171107004846/https://msdn.microsoft.com/en-us/library/dd905031.aspx) from the original on 7 November 2017. Retrieved 4 November 2017.
6. [↑](./Computation_of_cyclic_redundancy_checks#cite_ref-6) Kounavis, M.E.; Berry, F.L. (2005). "A Systematic Approach to Building High Performance Software-Based CRC Generators". [*10th IEEE Symposium on Computers and Communications (ISCC'05)*](https://static.aminer.org/pdf/PDF/000/432/446/a_systematic_approach_to_building_high_performance_software_based_crc.pdf) (PDF). pp. 855–862. [doi](./Doi_(identifier)):[10.1109/ISCC.2005.18](https://doi.org/10.1109%2FISCC.2005.18). [ISBN](./ISBN_(identifier)) [0-7695-2373-0](./Special:BookSources/0-7695-2373-0). [S2CID](./S2CID_(identifier)) [10308354](https://api.semanticscholar.org/CorpusID:10308354).
7. [↑](./Computation_of_cyclic_redundancy_checks#cite_ref-7) Berry, Frank L.; Kounavis, Michael E. (November 2008). "Novel Table Lookup-Based Algorithms for High-Performance CRC Generation". *IEEE Transactions on Computers*. **57** (11): 1550–1560. [Bibcode](./Bibcode_(identifier)):[2008ITCmp..57.1550K](https://ui.adsabs.harvard.edu/abs/2008ITCmp..57.1550K). [doi](./Doi_(identifier)):[10.1109/TC.2008.85](https://doi.org/10.1109%2FTC.2008.85). [S2CID](./S2CID_(identifier)) [206624854](https://api.semanticscholar.org/CorpusID:206624854).
8. [↑](./Computation_of_cyclic_redundancy_checks#cite_ref-8) [*High Octane CRC Generation with the Intel Slicing-by-8 Algorithm*](https://web.archive.org/web/20120722193753/http://download.intel.com/technology/comms/perfnet/download/slicing-by-8.pdf) (PDF) (Technical report). [Intel](./Intel). Archived from [the original](http://download.intel.com:80/technology/comms/perfnet/download/slicing-by-8.pdf) (PDF) on 2012-07-22.
9. [↑](./Computation_of_cyclic_redundancy_checks#cite_ref-9) ["Brief tutorial on CRC computation"](https://www.kernel.org/doc/Documentation/crc32.txt). *The Linux Kernel Archives*.
10. [↑](./Computation_of_cyclic_redundancy_checks#cite_ref-10) Menon-Sen, Abhijit (2017-01-20). ["Who invented the slicing-by-N CRC32 algorithm?"](http://toroid.org/crc32-slicing-by-N-paper).
11. [↑](./Computation_of_cyclic_redundancy_checks#cite_ref-11) Jon Buller (1996-03-15). ["Re: 8051 and CRC-CCITT"](https://groups.google.com/d/msg/comp.arch.embedded/fvQ7yM5F6ys/3xcgqF3Kqc4J). [Newsgroup](./Usenet_newsgroup): [comp.arch.embedded](news:comp.arch.embedded). [Usenet:](./Usenet_(identifier)) [31498ED0.7C0A@nortel.com](news:31498ED0.7C0A@nortel.com). Retrieved 2016-02-16.
12. [↑](./Computation_of_cyclic_redundancy_checks#cite_ref-12) AVR-LibC project (15 March 2024). ["AVR-LibC <util/crc16.h>"](https://avrdudes.github.io/avr-libc/avr-libc-user-manual/crc16_8h_source.html).
13. [↑](./Computation_of_cyclic_redundancy_checks#cite_ref-glaise_13-0) Glaise, René J. (1997-01-20). ["A two-step computation of cyclic redundancy code CRC-32 for ATM networks"](https://web.archive.org/web/20090130044254/http://www.research.ibm.com/journal/rd/416/glaise.html). *[IBM Journal of Research and Development](./IBM_Journal_of_Research_and_Development)*. **41** (6). [Armonk, NY](./Armonk,_NY): [IBM](./IBM): 705. [doi](./Doi_(identifier)):[10.1147/rd.416.0705](https://doi.org/10.1147%2Frd.416.0705). Archived from [the original](http://www.research.ibm.com/journal/rd/416/glaise.html) on 2009-01-30. Retrieved 2016-02-16.
14. [↑](./Computation_of_cyclic_redundancy_checks#cite_ref-14) Pei, Tong-Bi; Zukowsk, Charles (April 1992). "High-speed Parallel CRC Circuits in VLSI". *IEEE Transactions on Communications*. **40** (4): 653–657. [Bibcode](./Bibcode_(identifier)):[1992ITCom..40..653P](https://ui.adsabs.harvard.edu/abs/1992ITCom..40..653P). [doi](./Doi_(identifier)):[10.1109/26.141415](https://doi.org/10.1109%2F26.141415). While significant speedup can be achieved using parallel computation, simple multiplication by k is not quite achieved when *k* > 2. In fact, ⁠*k*/2⁠ (or more precisely [0.4*k*, 0.6*k*l) appears to be a reasonable model over a wide range of situations. With *k* = 8, we estimate that the prototype polynomial achieved a speedup of about 4.9.
15. [↑](./Computation_of_cyclic_redundancy_checks#cite_ref-15) Derby, Jeff H. (25–29 November 2001). *High-speed CRC computation using state-space transformations*. Global Telecommunications Conference. San Antonio, TX, USA. pp. 166–170. [doi](./Doi_(identifier)):[10.1109/GLOCOM.2001.965100](https://doi.org/10.1109%2FGLOCOM.2001.965100).
16. [1](./Computation_of_cyclic_redundancy_checks#cite_ref-Kennedy2009_16-0) [2](./Computation_of_cyclic_redundancy_checks#cite_ref-Kennedy2009_16-1) Kennedy, Christopher; Reyhani-Masoleh, Arash (7 June 2009). *High-speed CRC computations using improved state-space transformations*. IEEE International Conference on Electro/Information Technology. [doi](./Doi_(identifier)):[10.1109/EIT.2009.5189575](https://doi.org/10.1109%2FEIT.2009.5189575).
17. [↑](./Computation_of_cyclic_redundancy_checks#cite_ref-17) Das, Arindam (April 2023). "Block-wise computation of Cyclic Redundancy Code using factored Toeplitz matrices in lieu of Look-Up Table". *IEEE Transactions on Computers*. **72** (4): 1110–1121. [Bibcode](./Bibcode_(identifier)):[2023ITCmp..72.1110D](https://ui.adsabs.harvard.edu/abs/2023ITCmp..72.1110D). [doi](./Doi_(identifier)):[10.1109/TC.2022.3189574](https://doi.org/10.1109%2FTC.2022.3189574). [ISSN](./ISSN_(identifier)) [0018-9340](https://search.worldcat.org/issn/0018-9340). [S2CID](./S2CID_(identifier)) [250472783](https://api.semanticscholar.org/CorpusID:250472783).
18. [↑](./Computation_of_cyclic_redundancy_checks#cite_ref-Kadatch2010_18-0) Kadatch, Andrew; Jenkins, Bob (3 September 2010). [*Everything we know about CRC but afraid to forget*](https://github.com/rurban/crcutil/raw/master/doc/crc.pdf#page=4) (PDF) (Technical report). p. 4. The fact that the CRC of a message followed by its CRC is a constant value which does not depend on the message... is well known and has been widely used in the telecommunication industry for long time.  A good source for even more
19. [↑](./Computation_of_cyclic_redundancy_checks#cite_ref-19) E.g. low-frequency RFID [*TMS37157 data sheet - Passive Low Frequency Interface Device With EEPROM and 134.2 kHz Transponder Interface*](http://www.ti.com/lit/ds/symlink/tms37157.pdf) (PDF), [Texas Instruments](./Texas_Instruments), November 2009, p. 39, retrieved 2016-02-16, The CRC Generator is initialized with the value 0x3791 as shown in Figure 50.

 

## External links

 
- JohnPaul Adamovsky. ["64 Bit Cyclic Redundant Code – XOR Long Division To Bytewise Table Lookup"](http://pages.pathcom.com/~vadco/crc.html).

 
- Andrew Kadarch, Bob Jenkins. ["Efficient (~1 CPU cycle per byte) CRC implementation"](https://github.com/lizardfs/lizardfs/tree/master/external/crcutil-1.0). *[GitHub](./GitHub)*.