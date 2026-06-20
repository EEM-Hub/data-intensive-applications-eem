---
source: sources/wiki-Cyclic_redundancy_check.md
source_url: https://en.wikipedia.org/wiki/Cyclic_redundancy_check
---

## Cyclic Redundancy Check (CRC) — Error Detection via Polynomial Division

CRCs are error-detecting codes used in digital networks and storage to detect accidental data corruption. They work by computing a short, fixed-length check value (the remainder of a polynomial division over GF(2)) and appending it to a data block. On retrieval, the division is repeated; a non-zero remainder indicates corruption. CRCs are widely adopted because they are cheap in hardware, mathematically tractable, and excellent at catching burst errors common in real transmission channels.

## Key Concepts

- **Check value**: A fixed-length binary remainder computed from polynomial division of the data block; appended to form a codeword.
- **Generator polynomial**: The divisor in the polynomial long division. Its degree *n* determines the CRC width (an *n*-bit CRC uses an (*n*+1)-term polynomial). Selecting this polynomial is the most critical design decision.
- **GF(2) arithmetic**: All CRC math uses the finite field with two elements {0, 1}. Addition is XOR (no carry), making hardware implementation trivial.
- **Burst error detection**: An *n*-bit CRC detects any single burst error up to *n* bits long, and catches ~(1 − 2^−n) of longer bursts.
- **Systematic code**: The CRC is appended to the original data (data remains readable), and verification yields zero remainder when no errors are present.
- **Linearity/affine property**: CRC(x XOR y) = CRC(x) XOR CRC(y) XOR c. This makes CRC unsuitable for cryptographic integrity — an attacker can manipulate both message and CRC without knowing an encryption key (the WEP flaw).
- **Not a security mechanism**: CRCs detect accidental errors only. They are easily reversible, have no authentication, and must not substitute for cryptographic hash functions, MACs, or digital signatures.
- **Primitive polynomials**: Yield maximal block length (2^r − 1) where all 1-bit errors have distinct syndromes, enabling detection of all single-bit and double-bit errors within that length.
- **Multiplying by (1+x)**: Adding the factor (1+x) to a primitive polynomial of degree r−1 enables detection of all odd-bit-count errors, at the cost of halving the maximal block length to 2^(r−1) − 1.
- **Common CRC widths**: CRC-8 (9-bit poly), CRC-16 (17-bit), CRC-32 (33-bit), CRC-64 (65-bit).

## Commands and Syntax

**CRC computation algorithm (manual binary long division):**
1. Pad the message with *n* zero bits on the right (where *n* = CRC width).
2. Align the (n+1)-bit generator polynomial under the leftmost 1-bit of the padded message.
3. XOR the aligned bits; copy bits not under the polynomial unchanged.
4. Shift the polynomial right to align with the next leading 1-bit; repeat until the polynomial reaches the right end.
5. The remaining *n* bits are the CRC remainder.

**Verification:** Append the CRC to the original message (replacing the zero padding) and repeat the division. A zero remainder means no detectable error.

**Python reference implementation:**
```python
def crc_remainder(input_bitstring, polynomial_bitstring, initial_filler):
    polynomial_bitstring = polynomial_bitstring.lstrip("0")
    len_input = len(input_bitstring)
    initial_padding = (len(polynomial_bitstring) - 1) * initial_filler
    input_padded_array = list(input_bitstring + initial_padding)
    while "1" in input_padded_array[:len_input]:
        cur_shift = input_padded_array.index("1")
        for i in range(len(polynomial_bitstring)):
            input_padded_array[cur_shift + i] = str(
                int(polynomial_bitstring[i] != input_padded_array[cur_shift + i]))
    return "".join(input_padded_array)[len_input:]

# Example: 3-bit CRC with polynomial x^3 + x + 1 (binary "1011")
crc_remainder('11010011101100', '1011', '0')  # => '100'
```

**Polynomial notation conventions** (for x^4 + x + 1):
| Representation | Hex | What's omitted |
|---|---|---|
| Normal (MSB-first) | 0x3 | High-order bit (always 1) |
| Reversed (LSB-first) | 0xC | High-order bit, bit-reversed |
| Koopman | 0x9 | Low-order bit (always 1) |

**Specification complications to watch for:**
- Pre-inversion: fixed bit pattern prefixed to the bitstream
- Post-inversion: fixed pattern XORed into the remainder
- Bit order: LSb-first vs MSb-first (serial port conventions differ)
- Byte order: LSB vs MSB in multi-byte CRCs
- High-order or low-order bit omission in polynomial representation

## Relationships

- **Error-correcting codes**: CRCs are a subclass of cyclic codes, which are a family within error-correcting codes. They relate to BCH codes (a generalization for selecting polynomials that balance block length and detection power) and Hamming codes (CRC-32-IEEE's generator is a Hamming code polynomial).
- **Hash functions**: CRCs are occasionally repurposed as hash functions due to their fixed-length output, though they lack cryptographic properties.
- **Cryptographic hashes / MACs / digital signatures**: CRCs complement but do not replace these. For integrity against adversarial modification, use cryptographic mechanisms.
- **Stream ciphers (WEP)**: The affine linearity of CRC was exploited in WEP — XOR-based encryption preserves the ability to forge valid CRCs without the key.
- **Hardware instruction sets**: CRC-32C has dedicated instructions in Intel SSE4.2 (`CRC32` instruction, Nehalem onward) and ARM AArch64.
- **Protocols**: Ethernet, iSCSI, SCTP, G.hn, Gzip, Bzip2, and many others standardize specific CRC polynomials with varying pre/post-processing conventions.

## Exam-Relevant Points

- An *n*-bit CRC detects **any single burst error ≤ n bits** and approximately (1 − 2^−n) of longer bursts.
- CRC arithmetic uses **GF(2)** — addition is XOR with no carry.
- The generator polynomial has degree *n* and (*n*+1) terms for an *n*-bit CRC.
- **Verification**: append the CRC to the message, re-divide; remainder = 0 means no detectable error.
- CRCs detect errors but **do not provide authentication** — an attacker can recompute the CRC after altering data.
- CRC is an **affine function** over XOR, which means it is trivially forgeable under XOR-based encryption (the WEP vulnerability).
- A **primitive polynomial** of degree *r* gives maximal block length 2^r − 1 with all single- and double-bit errors detectable.
- Multiplying a primitive polynomial by (1+x) adds **odd-error detection** but halves the maximal block length.
- The simplest CRC is **CRC-1** (the parity bit), using generator polynomial x+1.
- CRC-32-IEEE and CRC-32C (Castagnoli) are the two most important 32-bit variants; CRC-32C outperforms IEEE at common Internet packet sizes and has hardware acceleration on Intel (SSE4.2) and ARM (AArch64).
- Polynomial representations differ by convention (Normal, Reversed, Koopman) — know that **one coefficient is always omitted** because it is always 1.
- The choice of polynomial depends on **maximum block length, desired Hamming distance, error distribution, and implementation resources** — not just irreducibility.
