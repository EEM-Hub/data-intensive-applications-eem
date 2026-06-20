---
source: https://en.wikipedia.org/wiki/Checksum
fetched: 2026-06-19
---

Data used to detect errors in other data 
|  | This articleneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sources. Unsourced material may be challenged and removed.Find sources:"Checksum"–news·newspapers·books·scholar·JSTOR(January 2024)(Learn how and when to remove this message) |
| --- | --- |

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/c/ce/Checksum.svg/330px-Checksum.svg.png)](./File:Checksum.svg)Effect of a typical checksum function (the Unix `cksum` utility) 

A **checksum** is a small-sized [block](./Block_(data_storage)) of data derived from another block of [digital data](./Digital_data) for the purpose of [detecting errors](./Error_detection) that may have been introduced during its [transmission](./Telecommunications) or [storage](./Computer_storage).  By themselves, checksums are often used to verify [data integrity](./Data_integrity) but are not relied upon to verify [data authenticity](./Data_authenticity).[[1]](./Checksum#cite_note-1)

 

The [procedure](./Algorithm) which generates this checksum is called a **checksum function** or **checksum algorithm**. Depending on its design goals, a good checksum algorithm usually outputs a significantly different value, even for small changes made to the input.[[2]](./Checksum#cite_note-2) This is especially true of [cryptographic hash functions](./Cryptographic_hash_function), which may be used to detect many data corruption errors and verify overall [data integrity](./Data_integrity); if the computed checksum for the current data input matches the stored value of a previously computed checksum, there is a very high probability the data has not been accidentally altered or corrupted.

 

Checksum functions are related to [hash functions](./Hash_function), [fingerprints](./Fingerprint_(computing)), [randomization functions](./Randomization_function), and [cryptographic hash functions](./Cryptographic_hash_function).  However, each of those concepts has different applications and therefore different design goals. For instance, a function returning the start of a string can provide a hash appropriate for some applications but will never be a suitable checksum. Checksums are used as [cryptographic primitives](./Cryptographic_primitive) in larger authentication algorithms. For cryptographic systems with these two specific design goals[*[clarification needed](./Wikipedia:Please_clarify)*], see [HMAC](./HMAC).

 

[Check digits](./Check_digit) and [parity bits](./Parity_bit) are special cases of checksums, appropriate for small blocks of data (such as [Social Security numbers](./Social_Security_number), [bank account](./Bank_account) numbers, [computer words](./Computer_word), single [bytes](./Byte), etc.).  Some [error-correcting codes](./Error-correcting_code) are based on special checksums which not only detect common errors but also allow the original data to be recovered in certain cases.

 

## Algorithms

 

### Parity byte or parity word

 

The simplest checksum algorithm is the so-called [longitudinal parity check](./Longitudinal_redundancy_check), which breaks the data into "words" with a fixed number *n* of bits, and then computes the bitwise [exclusive or](./Exclusive_or) (XOR) of all those words.  The result is appended to the message as an extra word. In simpler terms, for *n*=1 this means adding a bit to the end of the data bits to guarantee that there is an even number of '1's. To check the integrity of a message, the receiver computes the bitwise exclusive or of all its words, including the checksum; if the result is not a word consisting of *n* zeros, the receiver knows a transmission error occurred.[[3]](./Checksum#cite_note-3)

 

With this checksum, any transmission error which flips a single bit of the message, or an odd number of bits, will be detected as an incorrect checksum.  However, an error that affects two bits will not be detected if those bits lie at the same position in two distinct words.  Also swapping of two or more words will not be detected. If the affected bits are independently chosen at random, the probability of a two-bit error being undetected is 1/*n*.

 

### Sum complement

 

A variant of the previous algorithm is to add all the "words" as unsigned binary numbers, discarding any overflow bits, and append the [two's complement](./Two's_complement) of the total as the checksum.  To validate a message, the receiver adds all the words in the same manner, including the checksum; if the result is not a word full of zeros, an error must have occurred.  This variant, too, detects any single-bit error, but the pro modular sum is used in [SAE J1708](./SAE_J1708).[[4]](./Checksum#cite_note-4)

 

### Position-dependent

 

The simple checksums described above fail to detect some common errors which affect many bits at once, such as changing the order of data words, or inserting or deleting words with all bits set to zero.  The checksum algorithms most used in practice, such as [Fletcher's checksum](./Fletcher's_checksum), [Adler-32](./Adler-32), and [cyclic redundancy checks](./Cyclic_redundancy_check) (CRCs), address these weaknesses by considering not only the value of each word but also its position in the sequence. This feature generally increases the [cost](./Analysis_of_algorithms) of computing the checksum.

 

### Fuzzy checksum

 

The idea of fuzzy checksum was developed for detection of [email spam](./Email_spam) by building up cooperative databases from multiple ISPs of email suspected to be spam.   The content of such spam may often vary in its details, which would render normal checksumming ineffective.  By contrast, a "fuzzy checksum" reduces the body text to its characteristic minimum, then generates a checksum in the usual manner. This greatly increases the chances of slightly different spam emails producing the same checksum.  The ISP spam detection software, such as [SpamAssassin](./SpamAssassin), of co-operating ISPs, submits checksums of all emails to the centralised service such as [DCC](./Distributed_Checksum_Clearinghouse).  If the count of a submitted fuzzy checksum exceeds a certain threshold, the database notes that this probably indicates spam.  ISP service users similarly generate a fuzzy checksum on each of their emails and request the service for a spam likelihood.[[5]](./Checksum#cite_note-5)

 

### General considerations

 

A message that is *m* bits long can be viewed as a corner of the *m*-dimensional [hypercube](./Hypercube). The effect of a checksum algorithm that yields an *n*-bit checksum is to map each *m*-bit message to a corner of a larger hypercube, with dimension *m* + *n*. The 2*m* + *n* corners of this hypercube represent all possible received messages. The valid received messages (those that have the correct checksum) comprise a smaller set, with only 2*m* corners.

 

A single-bit transmission error then corresponds to a displacement from a valid corner (the correct message and checksum) to one of the *m* adjacent corners.  An error which affects *k* bits moves the message to a corner which is *k* steps removed from its correct corner.  The goal of a good checksum algorithm is to spread the valid corners as far from each other as possible, to increase the likelihood "typical" transmission errors will end up in an invalid corner.

 

## See also

  

**General topic**

 
- [Algorithm](./Algorithm)
- [Check digit](./Check_digit)
- [Damm algorithm](./Damm_algorithm)
- [Data rot](./Data_rot)
- [File verification](./File_verification)
- [Fletcher's checksum](./Fletcher's_checksum)
- [Frame check sequence](./Frame_check_sequence)
- [cksum](./Cksum)
- [md5sum](./Md5sum)
- [sha1sum](./Sha1sum)
- [Parchive](./Parchive)
- [Sum (Unix)](./Sum_(Unix))
- [SYSV checksum](./SYSV_checksum)
- [BSD checksum](./BSD_checksum)
- [xxHash](./XxHash)

 

**Error correction**

 
- [Hamming code](./Hamming_code)
- [Reed–Solomon error correction](./Reed–Solomon_error_correction)
- [IPv4 header checksum](./IPv4_header_checksum)

 

**Hash functions**

 
- [List of hash functions](./List_of_hash_functions)
- [Luhn algorithm](./Luhn_algorithm)
- [Parity bit](./Parity_bit)
- [Rolling checksum](./Rolling_checksum)
- [Verhoeff algorithm](./Verhoeff_algorithm)

 

**File systems**

 
- [Bcachefs](./Bcachefs), [Btrfs](./Btrfs), [ReFS](./ReFS) and [ZFS](./ZFS) – file systems that perform automatic file integrity checking using checksums

 

**Related concepts**

 
- [Isopsephy](./Isopsephy)
- [Gematria](./Gematria)
- [File fixity](./File_fixity)

  

## References

  
1. [↑](./Checksum#cite_ref-1) ["Definition of CHECKSUM"](https://www.merriam-webster.com/dictionary/checksum). *Merriam-Webster*. [Archived](https://web.archive.org/web/20220310132715/https://www.merriam-webster.com/dictionary/checksum) from the original on 2022-03-10. Retrieved 2022-03-10.
2. [↑](./Checksum#cite_ref-2) Hoffman, Chris (30 September 2019). ["What Is a Checksum (and Why Should You Care)?"](https://www.howtogeek.com/363735/what-is-a-checksum-and-why-should-you-care/). *How-To Geek*. [Archived](https://web.archive.org/web/20220309114058/https://www.howtogeek.com/363735/what-is-a-checksum-and-why-should-you-care/) from the original on 2022-03-09. Retrieved 2022-03-10.
3. [↑](./Checksum#cite_ref-3) Fairhurst, Gorry (2014). ["Checksums & Integrity Checks"](https://erg.abdn.ac.uk/users/gorry/eg3576/checksums.html). [Archived](https://web.archive.org/web/20220408011213/https://erg.abdn.ac.uk/users/gorry/eg3576/checksums.html) from the original on April 8, 2022. Retrieved March 11, 2022.
4. [↑](./Checksum#cite_ref-4) ["SAE J1708"](https://web.archive.org/web/20131211152639/http://www.kvaser.com/zh/about-can/related-protocols-and-standards/50.html). Kvaser.com. Archived from [the original](http://www.kvaser.com/zh/about-can/related-protocols-and-standards/50.html) on 11 December 2013.
5. [↑](./Checksum#cite_ref-5) ["IXhash"](https://cwiki.apache.org/confluence/display/spamassassin/iXhash). Apache. [Archived](https://web.archive.org/web/20200831125801/https://cwiki.apache.org/confluence/display/spamassassin/iXhash) from the original on 31 August 2020. Retrieved 7 January 2020.

 

## Further reading

 
- Koopman, Philip; Driscoll, Kevin; Hall, Brendan (March 2015). ["Cyclic Redundancy Code and Checksum Algorithms to Ensure Critical Data Integrity"](http://www.tc.faa.gov/its/worldpac/techrpt/tc14-49.pdf) (PDF). Federal Aviation Administration. DOT/FAA/TC-14/49. [Archived](https://web.archive.org/web/20150518073214/http://www.tc.faa.gov/its/worldpac/techrpt/tc14-49.pdf) (PDF) from the original on 2015-05-18.
- Koopman, Philip (2023). "Large-Block Modular Addition Checksum Algorithms". [arXiv](./ArXiv_(identifier)):[2302.13432](https://arxiv.org/abs/2302.13432) [[cs.DS](https://arxiv.org/archive/cs.DS)].

 

## External links

   [![Wikibooks logo](//upload.wikimedia.org/wikipedia/commons/thumb/f/fa/Wikibooks-logo.svg/40px-Wikibooks-logo.svg.png)](./File:Wikibooks-logo.svg) The Wikibook *[Algorithm Implementation](https://en.wikibooks.org/wiki/Algorithm%20Implementation)* has a page on the topic of: ***[Checksums](https://en.wikibooks.org/wiki/Algorithm%20Implementation/Checksums)***  
- [Additive Checksums (C)](https://barrgroup.com/blog/crc-series-part-1-additive-checksums) theory from Barr Group
- [Practical Application of Cryptographic Checksums](http://www.peterjockisch.de/texte/computerartikel/Kryptographische-Pruefsummen/Kryptographische-Pruefsummen_EN.html) *[A4](https://www.peterjockisch.de/Checksums_A4.pdf) *[US-Letter](https://www.peterjockisch.de/Checksums_US-Letter.pdf) *[US-Letter two-column](https://www.peterjockisch.de/Checksums_US-Letter_2.pdf)
- [Checksum Calculator](https://codebeautify.org/checksum-calculator)
- [Open source python based application with GUI used to verify downloads.](https://github.com/CRPrinzler/HASH-verify)