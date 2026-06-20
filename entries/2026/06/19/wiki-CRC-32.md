---
source: sources/wiki-CRC-32.md
source_url: https://en.wikipedia.org/wiki/CRC-32
---

## Computation of Cyclic Redundancy Checks

This page covers the practical implementation of CRC computation, progressing from the mathematical foundation (polynomial division modulo 2) through increasingly optimized algorithms: bit-at-a-time, byte-at-a-time with lookup tables, slicing-by-N parallel table lookups, and hardware-accelerated instructions. It also covers the critical practical details that cause real implementations to deviate from pure polynomial math — bit ordering, initial value presets, and post-inversion.

## Key Concepts

- CRC computation is polynomial long division over GF(2), where XOR replaces subtraction and there is no borrow/carry
- The "generator polynomial" defines the CRC variant; it is represented as a binary string with the leading coefficient often omitted (e.g., CRC-32 polynomial = 0x04C11DB7 msbit-first, 0xEDB88320 lsbit-first)
- An n-bit CRC uses an n-bit shift register to hold only the "interesting" intermediate bits during division
- The XOR of the generator polynomial is **deferred** — a message bit doesn't need to be mixed in until the moment it's tested; this eliminates the need to pad the message with n zero bits
- **Bit ordering (endianness)** is the most confusing practical aspect: msbit-first shifts left and tests the high bit; lsbit-first shifts right and tests the low bit. The reflected polynomial value differs accordingly
- **Preset to −1 (0xFFFF...)**: The initial remainder is complemented so that leading zero bytes affect the CRC, preventing the trivial weakness where prepending zeros doesn't change the checksum
- **Post-invert**: The final remainder is complemented so that appending zero bytes also affects the CRC; combined with preset, this means the CRC of a correct message+CRC is a fixed non-zero constant ("magic value" or "residue")
- **Lookup table optimization**: A 256-entry table memoizes 8 bits of division at once, replacing 8 conditional XOR iterations with a single table lookup + XOR
- **Table generation exploits linearity**: `table[i XOR j] = table[i] XOR table[j]`, so only entries for powers of two need direct computation (7 iterations for 256 entries)
- **Slicing-by-N**: Multiple bytes processed simultaneously using multiple tables (e.g., slicing-by-4 uses 4 tables of 256 entries), exploiting the fact that CRC XOR operations on non-overlapping byte positions are independent
- **Hardware acceleration**: Intel SSE 4.2 provides `PCLMULQDQ` (carry-less multiply) which can compute CRC-32C at near memory bandwidth speeds; ARM has similar CRC instructions

## Commands and Syntax

**Bit-at-a-time (core algorithm):**
```
rem := 0
for each bit b in message:
    if high bit of rem is set:
        rem := (rem << 1) XOR generator
    else:
        rem := rem << 1
    rem := rem XOR (b shifted to high position)
```

**Byte-at-a-time with table (msbit-first):**
```
rem = (rem << 8) XOR table[byte XOR (rem >> (n-8))]
```

**Byte-at-a-time with table (lsbit-first):**
```
rem = (rem >> 8) XOR table[byte XOR (rem & 0xFF)]
```

**CRC-32 complete (C, lsbit-first):**
```c
uint32_t crc32 = 0xFFFFFFFF;
for (i = 0; i < len; i++) {
    crc32 ^= data[i];
    crc32 = (crc32 >> 8) ^ CRCTable[crc32 & 0xFF];
}
crc32 ^= 0xFFFFFFFF;
```

**Table generation (lsbit-first, exploiting linearity):**
```c
crc32 = 1;
for (i = 128; i; i >>= 1) {
    crc32 = (crc32 >> 1) ^ (crc32 & 1 ? 0xEDB88320 : 0);
    for (j = 0; j < 256; j += 2*i)
        table[i+j] = crc32 ^ table[j];
}
```

## Relationships

- **Mathematics of CRC**: The theoretical foundation — polynomial arithmetic over GF(2), why certain polynomials detect certain error patterns
- **Shift registers / LFSRs**: Hardware CRC is literally a linear feedback shift register with XOR taps at polynomial coefficient positions
- **Endianness**: Bit ordering within bytes determines whether the implementation shifts left (msbit-first) or right (lsbit-first), and which polynomial representation to use
- **Error detection protocols**: Ethernet (IEEE 802.3), HDLC, USB, ZIP, PNG, and others all use specific CRC variants with defined preset/post-invert/bit-order conventions
- **Space-time tradeoffs**: The progression from bit-at-a-time (minimal memory) through 256-entry tables to slicing-by-8 (8KB of tables) to hardware instructions illustrates classic optimization tradeoffs
- **Two's complement / bitwise operations**: The "complement" steps (preset to −1, post-invert) are simple bitwise NOT on the register

## Exam-Relevant Points

- The CRC remainder of a correct message (data + appended CRC) is a **fixed constant** (the "residue"), not zero, when preset-to-−1 and post-invert are used — but it IS zero for "pure" polynomial division without these steps
- **Preset to −1 solves**: detection of added/removed leading zero bytes
- **Post-invert solves**: detection of added/removed trailing zero bytes
- The lsbit-first polynomial for CRC-32 is **0xEDB88320**; msbit-first is **0x04C11DB7** — these are bit-reversals of each other
- IEEE 802 (Ethernet) and RS-232 use **lsbit-first** transmission; floppy/hard disks use **msbit-first**
- Lookup table size 256 processes **8 bits per iteration**; table size 16 processes **4 bits** (useful for microcontrollers)
- The `table[i XOR j] = table[i] XOR table[j]` property means only **log2(256) = 8** direct CRC computations are needed to fill the entire table
- Slicing-by-4/8 achieves throughput of **one CRC-byte per clock cycle** on modern CPUs by exploiting independent byte-position processing
- CRC-32C (Castagnoli) is preferred over CRC-32 for new designs because it has better error detection and hardware acceleration support (Intel CRC32 instruction)
- A **two-byte-at-a-time** table (65536 entries) can be used when memory is plentiful, processing 16 bits per iteration
