---
source: sources/wiki-Variable-length_quantity.md
source_url: https://en.wikipedia.org/wiki/Variable-length_quantity
---

## Variable-Length Quantity (VLQ) Encoding

Variable-length quantity (VLQ) is a universal code that uses a variable number of bytes to represent arbitrarily large integers. It works as a base-128 encoding where each byte carries 7 bits of payload and uses the most significant bit (MSB) as a continuation flag — 1 means more bytes follow, 0 means this is the final byte. VLQ is identical to LEB128 except in endianness: VLQ is big-endian (most significant group first), while LEB128 is little-endian (least significant group first).

## Key Concepts

- **Base-128 encoding**: Each byte stores 7 bits of data, using bit 7 as a continuation marker. Also known as VByte, Varint, VInt, EncInt.
- **Continuation bit**: MSB of each octet — if 1, another octet follows; if 0, this is the last octet.
- **Compactness tradeoff**: Small integers use fewer bytes (e.g., 0–127 fit in 1 byte), while large integers expand as needed. This is the core benefit for storage-constrained or bandwidth-sensitive systems.
- **Redundancy problem**: Basic VLQ allows zero-padding by prepending `0x80` octets, meaning multiple encodings exist for the same value.
- **Git's bijective variant**: Eliminates redundancy by adding an offset to multi-byte VLQs so each integer has exactly one encoding. The minimum 2-byte VLQ starts at 128 (one past the 1-byte max of 127), making it a base-128 bijective numeration.
- **Group Varint Encoding (GVE)**: Google's optimization that uses a 1-byte header to describe the lengths of 4 following uint32 values, eliminating per-byte continuation-bit checks and reducing CPU branch mispredictions.
- **PrefixVarint**: Similar to GVE but supports uint64; reportedly invented independently multiple times.

## Signed Number Representations

- **Sign bit (Unreal Engine "Compact Indices")**: The first octet reserves bit 6 for sign, reducing payload of the first byte to 6 bits.
- **Zigzag encoding (Protocol Buffers)**: Maps signed integers to unsigned via `(n << 1) ^ (n >> k-1)`. Positive n maps to 2n, negative n maps to 2|n|−1. This interleaves positive and negative values (0, −1, 1, −2, 2, ...) so small-magnitude numbers always use few bytes regardless of sign.
- **Two's complement (LEB128/SLEB128)**: Sign-extends the input to a multiple of 7 bits, then encodes as usual. Used in DWARF debugging format.

## Commands and Syntax

**Encoding algorithm (decimal 137):**
1. Convert to binary: `10001001`
2. Split into 7-bit groups from LSB: `0000001` `0001001`
3. Last group (LSB) gets MSB=0: `0_0001001`
4. All other groups get MSB=1: `1_0000001`
5. Result (big-endian): `0x81 0x09`

**Zigzag transform:**
```
encoded = (n << 1) ^ (n >> (k - 1))   // k = bit width (e.g., 32)
```
- Positive: 0→0, 1→2, 2→4, 3→6
- Negative: −1→1, −2→3, −3→5

**Key encoding examples (MIDI spec):**
| Decimal | Hex | VLQ Hex |
|---------|-----|---------|
| 0 | 0x00 | `00` |
| 127 | 0x7F | `7F` |
| 128 | 0x80 | `81 00` |
| 16383 | 0x3FFF | `FF 7F` |
| 16384 | 0x4000 | `81 80 00` |
| 268435455 | 0x0FFFFFFF | `FF FF FF 7F` |

## Relationships

- **LEB128**: Little-endian counterpart of VLQ; used in DWARF and WebAssembly. Same structure, reversed byte order.
- **Protocol Buffers (varint)**: Google's wire format uses LEB128-style encoding with zigzag for signed integers (`sint32`/`sint64` types).
- **ASN.1 BER**: Uses base-128 for tag numbers and OID components — same continuation-bit scheme.
- **MIDI file format**: Original and canonical use case for VLQ; encodes delta-time values between events.
- **Git pack format**: Uses the bijective (non-redundant) VLQ variant for offset encoding.
- **Source maps**: JavaScript source maps use VLQ with base64 encoding (Base64-VLQ) to compactly represent line/column mappings.
- **LLVM bitstream format**: Uses variable-width integers with configurable chunk sizes (not necessarily 8-bit).
- **.NET BinaryReader/BinaryWriter**: `Read7BitEncodedInt` / `Write7BitEncodedInt` implement the same scheme.

## Exam-Relevant Points

- VLQ is big-endian (MSB group first); LEB128 is little-endian (LSB group first). This is the only difference between them.
- The continuation bit is the MSB (bit 7) of each byte: 1 = more bytes follow, 0 = last byte.
- Each byte carries exactly 7 bits of payload, giving base-128 representation.
- Basic VLQ is redundant (multiple encodings per value). Git's variant eliminates this via offset addition, creating a bijective numeration.
- Zigzag encoding formula: `(n << 1) ^ (n >> 31)` for 32-bit signed integers. It ensures small-magnitude negatives use few bytes — critical for Protocol Buffers efficiency.
- Group Varint Encoding improves decode throughput by eliminating per-byte branch checks, using a prefix byte to describe 4 value lengths at once.
- Maximum value in N bytes: 1 byte = 127, 2 bytes = 16383, 3 bytes = 2097151, 4 bytes = 268435455 (each step is 2^7 times the previous range minus 1).
- VLQ is only defined for unsigned integers in its basic form; signed representations (sign bit, zigzag, two's complement) are protocol-specific extensions.
