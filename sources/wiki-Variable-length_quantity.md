---
source: https://en.wikipedia.org/wiki/Variable-length_quantity
fetched: 2026-06-19
---

Encoding method for variable-length integers This article is about codes that are a variable number of bytes. For a more general category of variable-bit-length codes, see [variable-length code](./Variable-length_code). 

A **variable-length quantity** (**VLQ**) is a [universal code](./Universal_code_(data_compression)) that uses an arbitrary number of [binary](./Binary_code) [octets](./Octet_(computing)) (eight-[bit](./Bit) [bytes](./Byte)) to represent an arbitrarily large [integer](./Integer). A VLQ is essentially a base-128 representation of an unsigned integer with the addition of the eighth bit to mark continuation of bytes. VLQ is identical to [LEB128](./LEB128) except in [endianness](./Endianness). See the example below.

 

## Applications and history

 

Base-128 compression is known by many names – VB (Variable Byte), **VByte**, **Varint**, **VInt**, **EncInt** etc.[[1]](./Variable-length_quantity#cite_note-jianguo-1)

 

A **variable-length quantity** (**VLQ**) was defined for use in the standard [MIDI file](./MIDI_file) format[[2]](./Variable-length_quantity#cite_note-MIDI_File_Format-2) to save additional space for a resource-constrained system, and is also used in the later [Extensible Music Format (XMF)](./Extensible_Music_Format_(XMF)).

 

**Base-128** is also used in [ASN.1](./ASN.1) BER encoding to encode tag numbers and [object identifiers](./Object_identifier).[[3]](./Variable-length_quantity#cite_note-3) It is also used in the [WAP](./Wireless_Application_Protocol) environment, where it is called **variable length unsigned integer** or **uintvar**. RFC 6256 defines the same format and refers to it as a **Self-Delimiting Numeric Value** or **SDNV**.[[4]](./Variable-length_quantity#cite_note-rfc6256-4) The [DWARF](./DWARF) [debugging](./Debugging) format[[5]](./Variable-length_quantity#cite_note-5) defines a variant called [LEB128](./LEB128) (or **ULEB128** for unsigned numbers), where the least significant group of 7 bits is encoded in the first byte, and the most significant bits are in the last byte (so effectively it is the little-endian analog of a VLQ). [Google](./Google) [Protocol Buffers](./Protocol_Buffers) use a similar format to have compact representation of integer values,[[6]](./Variable-length_quantity#cite_note-6) as does [Oracle](./Oracle_Corporation) Portable Object Format (POF)[[7]](./Variable-length_quantity#cite_note-7) and the [Microsoft](./Microsoft) [.NET Framework](./.NET_Framework) "7-bit encoded int" in the **BinaryReader** and **BinaryWriter** classes.[[8]](./Variable-length_quantity#cite_note-8)

 

It is also used extensively in web browsers for source mapping – which contain a lot of integer line and column number mappings – to keep the size of the map to a minimum.[[9]](./Variable-length_quantity#cite_note-Introduction_to_javascript_source_maps-9)

 

Variable-width integers in [LLVM](./LLVM) use a similar principle. The encoding chunks are little-endian and need not be 8 bits in size. The LLVM documentation describes a field that uses 4-bit chunk, with each chunk consisting of 1 bit continuation and 3 bits payload.[[10]](./Variable-length_quantity#cite_note-10)

 

## Benefits

 
1. Compactness: One of the primary benefits of VLQ encoding is its compactness. Since it uses a variable number of bytes to encode an integer, smaller integers can be represented using fewer bytes, resulting in a smaller overall file size. This is particularly useful in scenarios where storage space is at a premium, such as in embedded systems or mobile devices.
2. Efficiency: VLQ encoding is an efficient way to store and transmit data. Since smaller integers are represented using fewer bytes, this reduces the amount of data that needs to be transmitted, which in turn reduces the time and bandwidth required to transmit the data.
3. Flexibility: Another advantage of VLQ encoding is its flexibility. Since the number of bytes used to represent an integer is based on its magnitude, VLQ encoding can handle integers of different sizes. This means that VLQ encoding can be used to represent integers of any size, from small 8-bit integers to large 64-bit integers.

 

## General structure

 

The encoding assumes an octet (an 8-bit byte) where the most significant bit (MSB), also commonly known as the [sign bit](./Sign_bit), is reserved to indicate whether another VLQ octet follows.

 
| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 27 | 26 | 25 | 24 | 23 | 22 | 21 | 20 |
| A | Bn |

 

If *A* is 0, then this is the last VLQ octet of the integer. If *A* is 1, then another VLQ octet follows.

 

*B* is a 7-bit number [0x00, 0x7F], and *n* is the position of the VLQ octet where *B*0 is [the least significant](./Endianness). The VLQ octets are arranged [most significant first](./Endianness) in a stream.

 

## Variants

 

The general VLQ encoding is simple, but in basic form is only defined for [unsigned integers](./Unsigned_integer) (nonnegative, positive or zero), and is somewhat redundant, since prepending 0x80 octets corresponds to zero padding. There are various [signed number representations](./Signed_number_representations) to handle negative numbers, and techniques to remove the redundancy.

 

### Group Varint Encoding

 

Google developed Group Varint Encoding (GVE) after observing that traditional VLQ encoding incurs many CPU branches during decompression. GVE uses a single byte as a header for 4 variable-length uint32 values. The header byte has 4 2-bit numbers representing the storage length of each of the following 4 uint32s. Such a layout eliminates the need to check and remove VLQ continuation bits.  Data bytes can be copied directly to their destination. This layout [ reduces CPU branches](./Branch_(computer_science)#Improving_performance_by_reducing_stalls_from_branches), making GVE faster than VLQ on modern pipelined CPUs.[[11]](./Variable-length_quantity#cite_note-dean-11)

 

PrefixVarint is a similar design but with a uint64 maximum. It is said to have "been invented multiple times independently".[[12]](./Variable-length_quantity#cite_note-12) It is possible to be changed into a chained version with infinitely many continuations.

 

### Signed numbers

 

#### Sign bit

 

Negative numbers can be handled using a [sign bit](./Sign_bit), which only needs to be present in the first octet.

 

In the data format for Unreal Packages used by the [Unreal Engine](./Unreal_Engine), a variable-length quantity scheme called Compact Indices[[13]](./Variable-length_quantity#cite_note-13) is used. The only difference in this encoding is that the first VLQ octet has the seventh bit reserved to indicate whether the encoded integer is positive or negative. Any consecutive VLQ octet follows the general structure.

 
| First VLQ octet | Other VLQ octets |
| --- | --- |
| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
| 27 | 26 | 25 | 24 | 23 | 22 | 21 | 20 | 27 | 26 | 25 | 24 | 23 | 22 | 21 | 20 |
| S | A | B0 | A | Bn(n> 0) |

 

If *S* is 0, then the VLQ represents a positive integer. If *S* is 1, then the VLQ represents a [negative number](./Negative_number).

 

If *A* is 0, then this is the last VLQ octet of the integer. If *A* is 1, then another VLQ octet follows.

 

*B* is the number chunk being encoded, and *n* is the position of the VLQ octet where *B*0 is [the least significant](./Endianness). The VLQ octets are arranged [least significant first](./Endianness) in a stream.

 

#### Zigzag encoding

 

An alternative way to encode negative numbers is to use the least significant bit for sign. This is notably done for Google Protocol Buffers, and is known as a **zigzag encoding** for [signed integers](./Signed_integer).[[14]](./Variable-length_quantity#cite_note-14) One can encode the numbers so that encoded 0 corresponds to 0, 1 to −1, 10 to 1, 11 to −2, 100 to 2, etc.: counting up alternates between nonnegative (starting at 0) and negative (since each step changes the least-significant bit, hence the sign), whence the name "zigzag encoding". Concretely, transform the integer as `(n << 1) ^ (n >> k - 1)` for fixed *k*-bit integers. This has the effect of:

 
- Mapping positive numbers to their multiples of two: `n << 1` is equivalent of `n x 2`. Example: 0, 1, 2, 3 are mapped to 0, 2, 4, 6.
- Mapping negative numbers to the positive odd numbers. A 32-bit negative integer has a form of `1xxx...`, so `n >> 31` fills all the bits with 1. XORing a [two's complement](./Two's_complement) negative number with all 1's turns it positive and subtracts 1. And remember that we multiplied the original number by 2 using `n << 1`. So -1, -2, -3 are mapped to 1, 3, 5.

 

#### Two's complement

 

LEB128 uses [two's complement](./Two's_complement) to represent signed numbers. In this scheme of representation, *n* bits encode a range from −2*n* to 2*n* − 1, and all negative numbers start with a 1 in the most significant bit. In Signed LEB128, the input is [sign-extended](./Sign_extension) so that its length is a multiple of 7 bits. From there the encoding proceeds as usual.[[15]](./Variable-length_quantity#cite_note-dwarfspec3-15)

 

In LEB128, the stream is arranged least significant first.[[15]](./Variable-length_quantity#cite_note-dwarfspec3-15)

 

### Removing redundancy

 

With the VLQ encoding described above, any number that can be encoded with N octets can also be encoded with more than N octets simply by prepending additional 0x80 octets as zero-padding. For example, the decimal number 358 can be encoded as the 2-octet VLQ 0x8266, or the number 0358 can be encoded as 3-octet VLQ 0x808266, or 00358 as the 4-octet VLQ 0x80808266 and so forth.

 

However, the VLQ format used in [Git](./Git_(software))[[16]](./Variable-length_quantity#cite_note-16) removes this prepending redundancy and extends the representable range of shorter VLQs by adding an offset to VLQs of 2 or more octets in such a way that the lowest possible value for such an (*N* + 1)-octet VLQ becomes exactly one more than the maximum possible value for an *N*-octet VLQ. In particular, since a 1-octet VLQ can store a maximum value of 127, the minimum 2-octet VLQ (0x8000) is assigned the value 128 instead of 0. Conversely, the maximum value of such a 2-octet VLQ (0xFF7F) is 16511 instead of just 16383. Similarly, the minimum 3-octet VLQ (0x808000) has a value of 16512 instead of zero, which means that the maximum 3-octet VLQ (0xFFFF7F) is 2113663 instead of just 2097151.

 

In this way, there is one and only one encoding of each integer, making this a base-128 [bijective numeration](./Bijective_numeration).

 

## Examples

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/c/c6/Uintvar_coding.svg/330px-Uintvar_coding.svg.png)](./File:Uintvar_coding.svg)Diagram showing how to convert 106903 from decimal to uintvar representation 

Here is a worked-out example for the decimal number [137](./137_(number)):

 
- Represent the value in binary notation (e.g. 137 as 10001001)
- Break it up in groups of 7 bits starting from the lowest significant bit (e.g. 137 as 0000001 0001001). This is equivalent to representing the number in [base](./Radix) 128.
- Take the lowest 7 bits, and that gives you the least significant byte (**0**000 1001). This byte comes last.
- For all the other groups of 7 bits (in the example, this is 000 0001), set the [MSb](./Most_significant_bit) to 1 (which gives **1**000 0001 in our example). Thus 137 becomes **1**000 0001 **0**000 1001, where the bits in boldface are something we added. These added bits denote whether there is another byte to follow or not. Thus, by definition, the very last byte of a variable-length integer will have 0 as its [MSb](./Most_significant_bit).

 

Another way to look at this is to represent the value in base-128 and then set the MSB of all but the last base-128 digit to 1.

 

The Standard MIDI [File format](./File_format) specification gives more examples:[[2]](./Variable-length_quantity#cite_note-MIDI_File_Format-2)[[17]](./Variable-length_quantity#cite_note-17) 

 
| Integer(decimal) | Integer (binary) | Variable-length quantity (binary) | Integer(hexadecimal) | Variable-lengthquantity(hexadecimal) |
| --- | --- | --- | --- | --- |
| 0 | 00000000 00000000 00000000 00000000 | 00000000 | 00000000 | 00 |
| 127 | 00000000 00000000 00000000 01111111 | 01111111 | 0000007F | 7F |
| 128 | 00000000 00000000 00000000 10000000 | 10000001 00000000 | 00000080 | 81 00 |
| 8192 | 00000000 00000000 00100000 00000000 | 11000000 00000000 | 00002000 | C0 00 |
| 16383 | 00000000 00000000 00111111 11111111 | 11111111 01111111 | 00003FFF | FF 7F |
| 16384 | 00000000 00000000 01000000 00000000 | 10000001 10000000 00000000 | 00004000 | 81 80 00 |
| 2097151 | 00000000 00011111 11111111 11111111 | 11111111 11111111 01111111 | 001FFFFF | FF FF 7F |
| 2097152 | 00000000 00100000 00000000 00000000 | 10000001 10000000 10000000 00000000 | 00200000 | 81 80 80 00 |
| 134217728 | 00001000 00000000 00000000 00000000 | 11000000 10000000 10000000 00000000 | 08000000 | C0 80 80 00 |
| 268435455 | 00001111 11111111 11111111 11111111 | 11111111 11111111 11111111 01111111 | 0FFFFFFF | FF FF FF 7F |

 

## References

  
1. [↑](./Variable-length_quantity#cite_ref-jianguo_1-0) Jianguo Wang; Chunbin Lin; Yannis Papakonstantinou; Steven Swanson.
["An Experimental Study of Bitmap Compression vs. Inverted List Compression"](http://db.ucsd.edu/wp-content/uploads/2017/03/sidm338-wangA.pdf) [Archived](https://web.archive.org/web/20191207005058/http://db.ucsd.edu/wp-content/uploads/2017/03/sidm338-wangA.pdf) 2019-12-07 at the [Wayback Machine](./Wayback_Machine).
2017.
[doi](./Doi_(identifier)):[10.1145/3035918.3064007](https://doi.org/10.1145%2F3035918.3064007).
2. [1](./Variable-length_quantity#cite_ref-MIDI_File_Format_2-0) [2](./Variable-length_quantity#cite_ref-MIDI_File_Format_2-1) [MIDI File Format: Variable Quantities](https://web.archive.org/web/20051129113105/http://www.borg.com/~jglatt/tech/midifile/vari.htm).
3. [↑](./Variable-length_quantity#cite_ref-3) ["ITU-T Recommendation X.690"](http://www.itu.int/ITU-T/studygroups/com17/languages/X.690-0207.pdf) (PDF). International Telecommunication Union. 2002.
4. [↑](./Variable-length_quantity#cite_ref-rfc6256_4-0) Eddy, Wesley M.; Davies, Elwyn (May 2011). [*Using Self-Delimiting Numeric Values in Protocols*](https://www.rfc-editor.org/rfc/rfc6256). [Internet Research Task Force](./Internet_Research_Task_Force). [doi](./Doi_(identifier)):[10.17487/RFC6256](https://doi.org/10.17487%2FRFC6256). [ISSN](./ISSN_(identifier)) [2070-1721](https://search.worldcat.org/issn/2070-1721). [RFC](./Request_for_Comments) [6256](https://datatracker.ietf.org/doc/html/rfc6256). *Informational.* 
5. [↑](./Variable-length_quantity#cite_ref-5) [DWARF Standard](http://www.dwarfstd.org/).
6. [↑](./Variable-length_quantity#cite_ref-6) [Google Protocol Buffers](https://code.google.com/apis/protocolbuffers/docs/encoding.html).
7. [↑](./Variable-length_quantity#cite_ref-7) [Oracle Portable Object Format (POF)](http://docs.oracle.com/cd/E14526_01/coh.350/e14509/apppifpof.htm) [Archived](https://web.archive.org/web/20131227133127/http://docs.oracle.com/cd/E14526_01/coh.350/e14509/apppifpof.htm) 2013-12-27 at the [Wayback Machine](./Wayback_Machine).
8. [↑](./Variable-length_quantity#cite_ref-8) [System.IO.BinaryWriter.Write7BitEncodedInt(int) method](http://msdn.microsoft.com/en-us/library/system.io.binarywriter.write7bitencodedint.aspx) and [System.IO.BinaryReader.Read7BitEncodedInt() method](http://msdn.microsoft.com/en-us/library/system.io.binaryreader.read7bitencodedint.aspx).
9. [↑](./Variable-length_quantity#cite_ref-Introduction_to_javascript_source_maps_9-0) [Introduction to javascript source maps](http://www.html5rocks.com/en/tutorials/developertools/sourcemaps/).
10. [↑](./Variable-length_quantity#cite_ref-10) ["LLVM Bitcode File Format", section "Variable Width Integers"](https://llvm.org/docs/BitCodeFormat.html#variable-width-value). Accessed 2019-10-01.
11. [↑](./Variable-length_quantity#cite_ref-dean_11-0)  Jeff Dean. ["Challenges in Building Large-Scale Information Retrieval Systems"](https://static.googleusercontent.com/media/research.google.com/en//people/jeff/WSDM09-keynote.pdf) (PDF). p. 58. Retrieved 2020-05-30.
12. [↑](./Variable-length_quantity#cite_ref-12) Olesen, Jakob Stoklund (31 May 2020). ["stoklund/varint"](https://web.archive.org/web/20201119135834/https://github.com/stoklund/varint#prefixvarint). Archived from [the original](https://github.com/stoklund/varint#prefixvarint) on 19 November 2020. Retrieved 9 July 2020.
13. [↑](./Variable-length_quantity#cite_ref-13) ["Unreal Packages"](https://web.archive.org/web/20100820185656/http://unreal.epicgames.com/Packages.htm). 1999-07-21. Archived from [the original](http://unreal.epicgames.com/Packages.htm) on 2010-08-20. Retrieved 2021-08-29.
14. [↑](./Variable-length_quantity#cite_ref-14) Protocol Buffers: Encoding: [Signed Integers](https://developers.google.com/protocol-buffers/docs/encoding#types).
15. [1](./Variable-length_quantity#cite_ref-dwarfspec3_15-0) [2](./Variable-length_quantity#cite_ref-dwarfspec3_15-1) Free Standards Group (December 2005). ["DWARF Debugging Information Format Specification Version 3.0"](http://dwarfstd.org/doc/Dwarf3.pdf) (PDF). p. 70. Retrieved 2009-07-19.
16. [↑](./Variable-length_quantity#cite_ref-16) ["Git – fast, scalable, distributed revision control system"](https://github.com/git/git/blob/7fb6aefd2aaffe66e614f7f7b83e5b7ab16d4806/varint.c#L4). 28 October 2021.
17. [↑](./Variable-length_quantity#cite_ref-17) [Standard MIDI-File Format Spec. 1.1](https://www.music.mcgill.ca/~ich/classes/mumt306/midiformat.pdf#page=2).

 

## External links

 
- [MIDI Manufacturers Association](http://www.midi.org/) (MMA) - Source for English-language MIDI specs
- [Association of Musical Electronics Industry](http://www.amei.or.jp/index_e.html) [Archived](https://web.archive.org/web/20100117000729/http://www.amei.or.jp/index_e.html) 2010-01-17 at the [Wayback Machine](./Wayback_Machine) (AMEI) -Source for Japanese-language MIDI specs