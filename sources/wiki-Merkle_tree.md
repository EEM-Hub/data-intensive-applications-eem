---
source: https://en.wikipedia.org/wiki/Merkle_tree
fetched: 2026-06-19
---

Type of data structure [![](//upload.wikimedia.org/wikipedia/commons/thumb/9/95/Hash_Tree.svg/500px-Hash_Tree.svg.png)](./File:Hash_Tree.svg)An example of a binary hash tree. Hashes 0-0 and 0-1 are the hash values of data blocks L1 and L2, respectively, and hash 0 is the hash of the concatenation of hashes 0-0 and 0-1. 

In [cryptography](./Cryptography) and [computer science](./Computer_science), a **hash tree** or **Merkle tree** is a [tree](./Tree_(data_structure)) in which every "leaf" [node](./Tree_(data_structure)#Terminology) is labelled with the [cryptographic hash](./Cryptographic_hash_function) of a data block, and every node that is not a leaf (called a *branch*, *inner node*, or *inode*) is labelled with the cryptographic hash of the labels of its child nodes. A hash tree allows efficient and secure verification of the contents of a large [data structure](./Data_structure). A hash tree is a generalization of a [hash list](./Hash_list) and a [hash chain](./Hash_chain).

 

Demonstrating that a leaf node is a part of a given binary hash tree requires computing a number of hashes proportional to the [logarithm](./Logarithm) of the number of leaf nodes in the tree.[[1]](./Merkle_tree#cite_note-1) Conversely, in a hash list, the number is proportional to the number of leaf nodes itself. A Merkle tree is therefore an efficient example of a [cryptographic commitment scheme](./Cryptographic_commitment#Partial_reveal), in which the root of the tree is seen as a commitment and leaf nodes may be revealed and proven to be part of the original commitment.[[2]](./Merkle_tree#cite_note-2)

 

The concept of a hash tree is named after [Ralph Merkle](./Ralph_Merkle), who patented it in 1979.[[3]](./Merkle_tree#cite_note-3)[[4]](./Merkle_tree#cite_note-4)

 

## Uses

 

Hash trees can be used to verify any kind of data stored, handled and transferred in and between computers. They can help ensure that data [blocks](./Blockchain) received from other peers in a [peer-to-peer network](./Peer-to-peer) are received undamaged and unaltered, and even to check that the other peers do not lie and send fake blocks.

 

Hash trees are used in: 

 
- [hash-based cryptography](./Hash-based_cryptography).
- [InterPlanetary File System](./InterPlanetary_File_System) (IPFS),
- [BitTorrent](./BitTorrent)
- hashtree[[5]](./Merkle_tree#cite_note-5)
- [ZFS](./ZFS) file system[[6]](./Merkle_tree#cite_note-endtoend-6) (to counter [data degradation](./Data_degradation)[[7]](./Merkle_tree#cite_note-7));
- [Dat](./Dat_(software)) protocol;
- [Apache Wave](./Apache_Wave) protocol;[[8]](./Merkle_tree#cite_note-8)
- [Git](./Git_(software)) and [Mercurial](./Mercurial) distributed revision control systems (although, strictly speaking, they use [directed acyclic graphs](./Directed_acyclic_graph), not trees);
- the [Tahoe-LAFS](./Tahoe-LAFS) backup system;
- [Zeronet](./Zeronet);
- [OpenZFS](./OpenZFS)[[9]](./Merkle_tree#cite_note-9)
- the [Bitcoin](./Bitcoin) and [Ethereum](./Ethereum) peer-to-peer networks;[[10]](./Merkle_tree#cite_note-10)
- the [Certificate Transparency](./Certificate_Transparency) framework;
- Merkle Tree Certificates;[[11]](./Merkle_tree#cite_note-11)
- the [Nix package manager](./Nix_package_manager) and descendants like [GNU Guix](./GNU_Guix);[[12]](./Merkle_tree#cite_note-12)
- a number of [NoSQL](./NoSQL) systems such as [Apache Cassandra](./Apache_Cassandra), [Riak](./Riak), and [Dynamo](./Dynamo_(storage_system)).[[13]](./Merkle_tree#cite_note-13)

 

Suggestions have been made to use hash trees in [trusted computing](./Trusted_computing) systems.[[14]](./Merkle_tree#cite_note-14)

 

## Overview

 

A hash tree is a [tree](./Binary_tree) of [hashes](./Hash_function) in which the leaves (i.e., leaf nodes, sometimes also called "leafs") are hashes of data [blocks](./Blockchain) in, for instance, a file or set of files. Nodes farther up in the tree are the hashes of their respective children. For example, in the above picture *hash 0* is the result of hashing the [concatenation](./Concatenation) of *hash 0-0* and *hash 0-1*. That is, *hash 0* = *hash*( *hash 0-0* + *hash 0-1* ) where "+" denotes concatenation.

 

Most hash tree implementations are binary (two child nodes under each node) but they can just as well use many more child nodes under each node.

 

Usually, a [cryptographic hash function](./Cryptographic_hash_function) such as [SHA-2](./SHA-2) is used for the hashing. If the hash tree only needs to protect against unintentional damage, non-cryptographic [checksums](./Checksum) such as [CRCs](./Cyclic_redundancy_check) can be used.

 

In the top of a hash tree there is a *top hash* (or *root hash* or *master hash*). Before downloading a file on a [P2P network](./P2P_network), in most cases the top hash is acquired from a trusted source, for instance a friend or a web site that is known to have good recommendations of files to download. When the top hash is available, the hash tree can be received from any non-trusted source, like any peer in the P2P network. Then, the received hash tree is checked against the trusted top hash, and if the hash tree is damaged or fake, another hash tree from another source will be tried until the program finds one that matches the top hash.[[15]](./Merkle_tree#cite_note-:0-15)

 

The main difference from a [hash list](./Hash_list) is that one branch of the hash tree can be downloaded at a time and the integrity of each branch can be checked immediately, even though the whole tree is not available yet. For example, in the picture, the integrity of *data block L2* can be verified immediately if the tree already contains *hash 0-0* and *hash 1* by hashing the data block and iteratively combining the result with *hash 0-0* and then *hash 1* and finally comparing the result with the *top hash*. Similarly, the integrity of *data block L3* can be verified if the tree already has *hash 1-1* and *hash 0*.  This can be an advantage since it is efficient to split files up in very small data blocks so that only small blocks have to be re-downloaded if they get damaged. If the hashed file is big, such a hash list or hash chain becomes fairly big. But if it is a tree, one small branch can be downloaded quickly, the integrity of the branch can be checked, and then the downloading of data blocks can start.[*[citation needed](./Wikipedia:Citation_needed)*]

 

### Second preimage attack

 

The Merkle hash root does not indicate the tree depth, enabling a [second-preimage attack](./Second-preimage_attack) in which an attacker creates a document other than the original that has the same Merkle hash root.  For the example above, an attacker can create a new document containing two data blocks, where the first is *hash 0-0* + *hash 0-1*, and the second is *hash 1-0* + *hash 1-1*.[[16]](./Merkle_tree#cite_note-16)[[17]](./Merkle_tree#cite_note-17)

 

One simple fix is defined in [Certificate Transparency](./Certificate_Transparency): when computing leaf node hashes, a 0x00 byte is prepended to the hash data, while 0x01 is prepended when computing internal node hashes.[[15]](./Merkle_tree#cite_note-:0-15)  Limiting the hash tree size is a prerequisite of some [formal security proofs](./Linked_timestamping#Provable_security), and helps in making some proofs tighter. Some implementations limit the tree depth using hash tree depth prefixes before hashes, so any extracted hash chain is defined to be valid only if the prefix decreases at each step and is still positive when the leaf is reached.

 

### Tiger tree hash

 

The Tiger tree hash is a widely used form of hash tree. It uses a binary hash tree (two child nodes under each node), usually has a data block size of 1024 [bytes](./Byte) and uses the [Tiger hash](./Tiger_(hash_function)).[[18]](./Merkle_tree#cite_note-18)

 

Tiger tree hashes are used in [Gnutella](./Gnutella),[[19]](./Merkle_tree#cite_note-19) [Gnutella2](./Gnutella2), and [Direct Connect](./Direct_Connect_(file_sharing)) [P2P](./Peer-to-peer) file sharing protocols[[20]](./Merkle_tree#cite_note-20) and in [file sharing](./File_sharing) applications such as [Phex](./Phex),[[21]](./Merkle_tree#cite_note-21) [BearShare](./BearShare), [LimeWire](./LimeWire), [Shareaza](./Shareaza), [DC++](./DCPlusPlus)[[22]](./Merkle_tree#cite_note-22) and [gtk-gnutella](./Gtk-gnutella).[[23]](./Merkle_tree#cite_note-23)

 

## See also

 
- [![icon](//upload.wikimedia.org/wikipedia/commons/thumb/6/6f/Octicons-terminal.svg/40px-Octicons-terminal.svg.png)](./File:Octicons-terminal.svg)[Computer programming portal](./Portal:Computer_programming)

 
- [Binary tree](./Binary_tree)
- [Blockchain](./Blockchain)
- [Distributed hash table](./Distributed_hash_table)
- [Hash table](./Hash_table)
- [Hash trie](./Hash_trie)
- [Linked timestamping](./Linked_timestamping)
- [Radix tree](./Radix_tree)

 

## References

  
1. [↑](./Merkle_tree#cite_ref-1) Becker, Georg (2008-07-18). ["Merkle Signature Schemes, Merkle Trees and Their Cryptanalysis"](https://web.archive.org/web/20141222120036/http://www.emsec.rub.de/media/crypto/attachments/files/2011/04/becker_1.pdf) (PDF). Ruhr-Universität Bochum. p. 16. Archived from [the original](http://www.emsec.rub.de/media/crypto/attachments/files/2011/04/becker_1.pdf) (PDF) on 2014-12-22. Retrieved 2013-11-20.
2. [↑](./Merkle_tree#cite_ref-2) ["Handbook of Applied Cryptography"](https://cacr.uwaterloo.ca/hac/). *cacr.uwaterloo.ca*. Section 13.4.1. Retrieved 2024-03-07.
3. [↑](./Merkle_tree#cite_ref-3) Merkle, R. C. (1988). "A Digital Signature Based on a Conventional Encryption Function". *Advances in Cryptology – CRYPTO '87*. Lecture Notes in Computer Science. Vol. 293. pp. 369–378. [doi](./Doi_(identifier)):[10.1007/3-540-48184-2_32](https://doi.org/10.1007%2F3-540-48184-2_32). [ISBN](./ISBN_(identifier)) [978-3-540-18796-7](./Special:BookSources/978-3-540-18796-7).
4. [↑](./Merkle_tree#cite_ref-4) [US patent 4309569](https://worldwide.espacenet.com/textdoc?DB=EPODOC&IDX=US4309569), Ralph Merkle, "Method of providing digital signatures", published Jan 5, 1982,  assigned to The Board of Trustees of the Leland Stanford Junior University 
5. [↑](./Merkle_tree#cite_ref-5) ["hashtree developer page"](https://hashtree.cc/#/dev).
6. [↑](./Merkle_tree#cite_ref-endtoend_6-0) Bonwick, Jeff (2005-12-08). ["ZFS End-to-End Data Integrity"](https://blogs.oracle.com/bonwick/entry/zfs_end_to_end_data). *blogs.oracle.com*. [Archived](https://web.archive.org/web/20120403015447/https://blogs.oracle.com/bonwick/entry/zfs_end_to_end_data) from the original on April 3, 2012. Retrieved 2013-09-19.
7. [↑](./Merkle_tree#cite_ref-7) Likai Liu. ["Bitrot Resistance on a Single Drive"](http://lifecs.likai.org/2014/06/bitrot-resistance-on-single-drive.html). *likai.org*.
8. [↑](./Merkle_tree#cite_ref-8) ["General Verifiable Federation"](https://web.archive.org/web/20180408150608/http://www.waveprotocol.org/whitepapers/wave-protocol-verification). *Google Wave Protocol*. Archived from [the original](http://www.waveprotocol.org/whitepapers/wave-protocol-verification) on 2018-04-08. Retrieved 2017-03-09.
9. [↑](./Merkle_tree#cite_ref-9) ["Introduction to ZFS — openzfs latest documentation"](https://openzfs.readthedocs.io/en/latest/introduction.html). *openzfs.readthedocs.io*. Retrieved 2025-05-27.
10. [↑](./Merkle_tree#cite_ref-10) Koblitz, Neal; Menezes, Alfred J. (January 2016). "Cryptocash, cryptocurrencies, and cryptocontracts". *Designs, Codes and Cryptography*. **78** (1): 87–102. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.701.8721](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.701.8721). [doi](./Doi_(identifier)):[10.1007/s10623-015-0148-5](https://doi.org/10.1007%2Fs10623-015-0148-5). [S2CID](./S2CID_(identifier)) [16594958](https://api.semanticscholar.org/CorpusID:16594958).
11. [↑](./Merkle_tree#cite_ref-11) D. Benjamin; D. O'Brien; B. E. Westerbaan; L. Valenta; F. Valsorda (2026-05-24). ["Merkle Tree Certificates"](https://datatracker.ietf.org/doc/draft-ietf-plants-merkle-tree-certs/). *Internet Engineering Task Force*. IETF. Retrieved 2026-06-11.
12. [↑](./Merkle_tree#cite_ref-12) Dolstra, E. [*The Purely Functional Software Deployment Model.*](https://nixos.org/~eelco/pubs/phd-thesis.pdf#page21) PhD thesis, Faculty of Science, Utrecht, The Netherlands. January 2006. p.21 [ISBN](./ISBN_(identifier)) [90-393-4130-3](./Special:BookSources/90-393-4130-3).
13. [↑](./Merkle_tree#cite_ref-13) Adam Marcus. ["The NoSQL Ecosystem"](http://www.aosabook.org/en/nosql.html). *aosabook.org*. When a replica is down for an extended period of time, or the machine storing hinted handoffs for an unavailable replica goes down as well, replicas must synchronize from one another. In this case, Cassandra and Riak implement a Dynamo-inspired process called anti-entropy. In anti-entropy, replicas exchange Merkle trees to identify parts of their replicated key ranges which are out of sync. A Merkle tree is a hierarchical hash verification: if the hash over the entire keyspace is not the same between two replicas, they will exchange hashes of smaller and smaller portions of the replicated keyspace until the out-of-sync keys are identified. This approach reduces unnecessary data transfer between replicas which contain mostly similar data.
14. [↑](./Merkle_tree#cite_ref-14) Kilian, J. (1995). ["Improved Efficient Arguments"](https://link.springer.com/content/pdf/10.1007/3-540-44750-4_25.pdf) (PDF). *Advances in Cryptology — CRYPT0' 95*. Lecture Notes in Computer Science. Vol. 963. pp. 311–324. [doi](./Doi_(identifier)):[10.1007/3-540-44750-4_25](https://doi.org/10.1007%2F3-540-44750-4_25). [ISBN](./ISBN_(identifier)) [978-3-540-60221-7](./Special:BookSources/978-3-540-60221-7).
15. [1](./Merkle_tree#cite_ref-:0_15-0) [2](./Merkle_tree#cite_ref-:0_15-1) Laurie, B.; Langley, A.; Kasper, E. (June 2013). ["Certificate Transparency"](https://www.rfc-editor.org/info/rfc6962). *IETF* RFC6962. [doi](./Doi_(identifier)):[10.17487/rfc6962](https://doi.org/10.17487%2Frfc6962).
16. [↑](./Merkle_tree#cite_ref-16) Elena Andreeva; Charles Bouillaguet; Orr Dunkelman; John Kelsey (January 2009). "Herding, Second Preimage and Trojan Message Attacks beyond Merkle-Damgård". *Selected Areas in Cryptography*. Lecture Notes in Computer Science. Vol. 5867. SAC. pp. 393–414. [doi](./Doi_(identifier)):[10.1007/978-3-642-05445-7_25](https://doi.org/10.1007%2F978-3-642-05445-7_25). [ISBN](./ISBN_(identifier)) [978-3-642-05443-3](./Special:BookSources/978-3-642-05443-3).
17. [↑](./Merkle_tree#cite_ref-17) Elena Andreeva; Charles Bouillaguet; Pierre-Alain Fouque; Jonathan J. Hoch; John Kelsey; Adi Shamir; Sebastien Zimmer (2008). "Second Preimage Attacks on Dithered Hash Functions". In Smart, Nigel (ed.). *Advances in Cryptology – EUROCRYPT 2008*. Lecture Notes in Computer Science. Vol. 4965. Istanbul, Turkey. pp. 270–288. [doi](./Doi_(identifier)):[10.1007/978-3-540-78967-3_16](https://doi.org/10.1007%2F978-3-540-78967-3_16). [ISBN](./ISBN_(identifier)) [978-3-540-78966-6](./Special:BookSources/978-3-540-78966-6). [S2CID](./S2CID_(identifier)) [12844017](https://api.semanticscholar.org/CorpusID:12844017).`{{cite book}}`:  CS1 maint: location missing publisher ([link](./Category:CS1_maint:_location_missing_publisher))
18. [↑](./Merkle_tree#cite_ref-18) Chapweske, J.; Mohr, G. (March 4, 2003). ["Tree Hash EXchange format (THEX)"](https://web.archive.org/web/20090803220648/http://open-content.net/specs/draft-jchapweske-thex-02.html). Archived from the original on 2009-08-03.
19. [↑](./Merkle_tree#cite_ref-19) ["tigertree.c File Reference"](https://gtk-gnutella.sourceforge.net/doxygen/tigertree_8c.html). *Gtk-Gnutella*. Retrieved 23 September 2018.
20. [↑](./Merkle_tree#cite_ref-20) ["Audit: P2P DirectConnect Application"](https://web.archive.org/web/20150129050053/http://www.symantec.com/security_response/attacksignatures/detail.jsp?asid=21587). *Symantec*. Archived from [the original](https://www.symantec.com/security_response/attacksignatures/detail.jsp?asid=21587) on January 29, 2015. Retrieved 23 September 2018.
21. [↑](./Merkle_tree#cite_ref-21) Arne Babenhauserheide (7 Jan 2007). ["Phex 3.0.0 released"](http://www.phex.org/mambo/content/view/80/2/). *Phex*. Retrieved 23 September 2018.
22. [↑](./Merkle_tree#cite_ref-22) ["DC++'s feature list"](http://dcplusplus.sourceforge.net/features.html). *dcplusplus.sourceforge.net*.
23. [↑](./Merkle_tree#cite_ref-23) ["Development"](http://gtk-gnutella.sourceforge.net/en/?page=devel). *GTK-Gnutella*. Retrieved 23 September 2018.

 

## Further reading

 
- [Merkle tree patent 4,309,569](https://patents.google.com/patent/US4309569) –  explains both the hash tree structure and the use of it to handle many one-time signatures
- [Tree Hash EXchange format (THEX)](https://web.archive.org/web/20080316033726/http://www.open-content.net/specs/draft-jchapweske-thex-02.html) –  a detailed description of Tiger trees

 

## External links

 Listen to this article (5 minutes) ![Spoken Wikipedia icon](//upload.wikimedia.org/wikipedia/commons/thumb/8/87/Gnome-mime-sound-openclipart.svg/60px-Gnome-mime-sound-openclipart.svg.png)[This audio file](./File:En-Merkle_Tree.ogg) was created from a revision of this article dated 17 September 2013 (2013-09-17), and does not reflect subsequent edits.([Audio help](./Wikipedia:Media_help) · [More spoken articles](./Wikipedia:Spoken_articles)) 
- [A C implementation of a dynamically re-sizeable binary SHA-256 hash tree (Merkle tree)](https://github.com/IAIK/merkle-tree)
- [Merkle tree implementation in Java](https://github.com/richpl/merkletree)
- [Tiger Tree Hash (TTH) source code in C#](https://www.codeproject.com/articles/9336/thexcs-tth-tiger-tree-hash-maker-in-c), by Gil Schmidt
- [Tiger Tree Hash (TTH) implementations in C and Java](https://sourceforge.net/projects/tigertree/)
- [RHash](https://rhash.sourceforge.net/), an open source command-line tool, which can calculate TTH and magnet links with TTH

 
| vteCryptographic hash functionsandmessage authentication codesListComparisonKnown attacksCommon functionsMD5(compromised)SHA-1(compromised)SHA-2SHA-3BLAKE2SHA-3 finalistsBLAKEGrøstlJHSkeinKeccak(winner)Other functionsBLAKE3CubeHashECOHFSBFugueGOSTHAS-160HAVALKupynaLSHLaneMASH-1MASH-2MD2MD4MD6MDC-2N-hashRIPEMDRadioGatúnSIMDSM3SWIFFTShabalSnefruStreebogTigerVSHWhirlpoolPassword hashing/key stretchingfunctionsArgon2BalloonbcryptCatenacryptLM hashLyra2MakwaPBKDF2scryptyescryptGeneral purposekey derivation functionsHKDFKDF1/KDF2MAC functionsCBC-MACDAAGMACHMACNMACOMAC/CMACPMACPoly1305SipHashUMACVMACAuthenticatedencryptionmodesCCMChaCha20-Poly1305CWCEAXGCMIAPMOCBAttacksCollision attackPreimage attackBirthday attackBrute-force attackRainbow tableSide-channel attackLength extension attackDesignAvalanche effectHash collisionMerkle–Damgård constructionSponge functionHAIFA constructionStandardizationCAESAR CompetitionCRYPTRECNESSIENIST hash function competitionPassword Hashing CompetitionNSA Suite BCNSAUtilizationHash-based cryptographyMerkle treeMessage authenticationProof of workSaltPepper | vteCryptographic hash functionsandmessage authentication codesListComparisonKnown attacksCommon functionsMD5(compromised)SHA-1(compromised)SHA-2SHA-3BLAKE2SHA-3 finalistsBLAKEGrøstlJHSkeinKeccak(winner)Other functionsBLAKE3CubeHashECOHFSBFugueGOSTHAS-160HAVALKupynaLSHLaneMASH-1MASH-2MD2MD4MD6MDC-2N-hashRIPEMDRadioGatúnSIMDSM3SWIFFTShabalSnefruStreebogTigerVSHWhirlpoolPassword hashing/key stretchingfunctionsArgon2BalloonbcryptCatenacryptLM hashLyra2MakwaPBKDF2scryptyescryptGeneral purposekey derivation functionsHKDFKDF1/KDF2MAC functionsCBC-MACDAAGMACHMACNMACOMAC/CMACPMACPoly1305SipHashUMACVMACAuthenticatedencryptionmodesCCMChaCha20-Poly1305CWCEAXGCMIAPMOCBAttacksCollision attackPreimage attackBirthday attackBrute-force attackRainbow tableSide-channel attackLength extension attackDesignAvalanche effectHash collisionMerkle–Damgård constructionSponge functionHAIFA constructionStandardizationCAESAR CompetitionCRYPTRECNESSIENIST hash function competitionPassword Hashing CompetitionNSA Suite BCNSAUtilizationHash-based cryptographyMerkle treeMessage authenticationProof of workSaltPepper | vteCryptographic hash functionsandmessage authentication codes | ListComparisonKnown attacks | Common functions | MD5(compromised)SHA-1(compromised)SHA-2SHA-3BLAKE2 | SHA-3 finalists | BLAKEGrøstlJHSkeinKeccak(winner) | Other functions | BLAKE3CubeHashECOHFSBFugueGOSTHAS-160HAVALKupynaLSHLaneMASH-1MASH-2MD2MD4MD6MDC-2N-hashRIPEMDRadioGatúnSIMDSM3SWIFFTShabalSnefruStreebogTigerVSHWhirlpool | Password hashing/key stretchingfunctions | Argon2BalloonbcryptCatenacryptLM hashLyra2MakwaPBKDF2scryptyescrypt | General purposekey derivation functions | HKDFKDF1/KDF2 | MAC functions | CBC-MACDAAGMACHMACNMACOMAC/CMACPMACPoly1305SipHashUMACVMAC | Authenticatedencryptionmodes | CCMChaCha20-Poly1305CWCEAXGCMIAPMOCB | Attacks | Collision attackPreimage attackBirthday attackBrute-force attackRainbow tableSide-channel attackLength extension attack | Design | Avalanche effectHash collisionMerkle–Damgård constructionSponge functionHAIFA construction | Standardization | CAESAR CompetitionCRYPTRECNESSIENIST hash function competitionPassword Hashing CompetitionNSA Suite BCNSA | Utilization | Hash-based cryptographyMerkle treeMessage authenticationProof of workSaltPepper |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| vteCryptographic hash functionsandmessage authentication codesListComparisonKnown attacksCommon functionsMD5(compromised)SHA-1(compromised)SHA-2SHA-3BLAKE2SHA-3 finalistsBLAKEGrøstlJHSkeinKeccak(winner)Other functionsBLAKE3CubeHashECOHFSBFugueGOSTHAS-160HAVALKupynaLSHLaneMASH-1MASH-2MD2MD4MD6MDC-2N-hashRIPEMDRadioGatúnSIMDSM3SWIFFTShabalSnefruStreebogTigerVSHWhirlpoolPassword hashing/key stretchingfunctionsArgon2BalloonbcryptCatenacryptLM hashLyra2MakwaPBKDF2scryptyescryptGeneral purposekey derivation functionsHKDFKDF1/KDF2MAC functionsCBC-MACDAAGMACHMACNMACOMAC/CMACPMACPoly1305SipHashUMACVMACAuthenticatedencryptionmodesCCMChaCha20-Poly1305CWCEAXGCMIAPMOCBAttacksCollision attackPreimage attackBirthday attackBrute-force attackRainbow tableSide-channel attackLength extension attackDesignAvalanche effectHash collisionMerkle–Damgård constructionSponge functionHAIFA constructionStandardizationCAESAR CompetitionCRYPTRECNESSIENIST hash function competitionPassword Hashing CompetitionNSA Suite BCNSAUtilizationHash-based cryptographyMerkle treeMessage authenticationProof of workSaltPepper | vteCryptographic hash functionsandmessage authentication codes | ListComparisonKnown attacks | Common functions | MD5(compromised)SHA-1(compromised)SHA-2SHA-3BLAKE2 | SHA-3 finalists | BLAKEGrøstlJHSkeinKeccak(winner) | Other functions | BLAKE3CubeHashECOHFSBFugueGOSTHAS-160HAVALKupynaLSHLaneMASH-1MASH-2MD2MD4MD6MDC-2N-hashRIPEMDRadioGatúnSIMDSM3SWIFFTShabalSnefruStreebogTigerVSHWhirlpool | Password hashing/key stretchingfunctions | Argon2BalloonbcryptCatenacryptLM hashLyra2MakwaPBKDF2scryptyescrypt | General purposekey derivation functions | HKDFKDF1/KDF2 | MAC functions | CBC-MACDAAGMACHMACNMACOMAC/CMACPMACPoly1305SipHashUMACVMAC | Authenticatedencryptionmodes | CCMChaCha20-Poly1305CWCEAXGCMIAPMOCB | Attacks | Collision attackPreimage attackBirthday attackBrute-force attackRainbow tableSide-channel attackLength extension attack | Design | Avalanche effectHash collisionMerkle–Damgård constructionSponge functionHAIFA construction | Standardization | CAESAR CompetitionCRYPTRECNESSIENIST hash function competitionPassword Hashing CompetitionNSA Suite BCNSA | Utilization | Hash-based cryptographyMerkle treeMessage authenticationProof of workSaltPepper |
| vteCryptographic hash functionsandmessage authentication codes |
| ListComparisonKnown attacks |
| Common functions | MD5(compromised)SHA-1(compromised)SHA-2SHA-3BLAKE2 |
| SHA-3 finalists | BLAKEGrøstlJHSkeinKeccak(winner) |
| Other functions | BLAKE3CubeHashECOHFSBFugueGOSTHAS-160HAVALKupynaLSHLaneMASH-1MASH-2MD2MD4MD6MDC-2N-hashRIPEMDRadioGatúnSIMDSM3SWIFFTShabalSnefruStreebogTigerVSHWhirlpool |
| Password hashing/key stretchingfunctions | Argon2BalloonbcryptCatenacryptLM hashLyra2MakwaPBKDF2scryptyescrypt |
| General purposekey derivation functions | HKDFKDF1/KDF2 |
| MAC functions | CBC-MACDAAGMACHMACNMACOMAC/CMACPMACPoly1305SipHashUMACVMAC |
| Authenticatedencryptionmodes | CCMChaCha20-Poly1305CWCEAXGCMIAPMOCB |
| Attacks | Collision attackPreimage attackBirthday attackBrute-force attackRainbow tableSide-channel attackLength extension attack |
| Design | Avalanche effectHash collisionMerkle–Damgård constructionSponge functionHAIFA construction |
| Standardization | CAESAR CompetitionCRYPTRECNESSIENIST hash function competitionPassword Hashing CompetitionNSA Suite BCNSA |
| Utilization | Hash-based cryptographyMerkle treeMessage authenticationProof of workSaltPepper |
| vteCryptographyGeneralHistory of cryptographyOutline of cryptographyClassical cipherCryptographic protocolAuthentication protocolCryptographic primitiveCryptanalysisCryptocurrencyCryptosystemCryptographic nonceCryptovirologyHash functionCryptographic hash functionKey derivation functionSecure Hash AlgorithmsDigital signatureKleptographyKey (cryptography)Key exchangeKey generatorKey scheduleKey stretchingKeygenMachinesRansomwareRandom number generationCryptographically secure pseudorandom number generator(CSPRNG)Pseudorandom noise(PRN)Secure channelInsecure channelSubliminal channelEncryptionDecryptionEnd-to-end encryptionHarvest now, decrypt laterInformation-theoretic securityPlaintextCodetextCiphertextShared secretTrapdoor functionTrusted timestampingKey-based routingOnion routingGarlic routingKademliaMix networkMathematicsCryptographic hash functionBlock cipherStream cipherSymmetric-key algorithmAuthenticated encryptionPublic-key cryptographyQuantum key distributionQuantum cryptographyPost-quantum cryptographyMessage authentication codeRandom numbersSteganographyCategory | vteCryptography | General | History of cryptographyOutline of cryptographyClassical cipherCryptographic protocolAuthentication protocolCryptographic primitiveCryptanalysisCryptocurrencyCryptosystemCryptographic nonceCryptovirologyHash functionCryptographic hash functionKey derivation functionSecure Hash AlgorithmsDigital signatureKleptographyKey (cryptography)Key exchangeKey generatorKey scheduleKey stretchingKeygenMachinesRansomwareRandom number generationCryptographically secure pseudorandom number generator(CSPRNG)Pseudorandom noise(PRN)Secure channelInsecure channelSubliminal channelEncryptionDecryptionEnd-to-end encryptionHarvest now, decrypt laterInformation-theoretic securityPlaintextCodetextCiphertextShared secretTrapdoor functionTrusted timestampingKey-based routingOnion routingGarlic routingKademliaMix network | Mathematics | Cryptographic hash functionBlock cipherStream cipherSymmetric-key algorithmAuthenticated encryptionPublic-key cryptographyQuantum key distributionQuantum cryptographyPost-quantum cryptographyMessage authentication codeRandom numbersSteganography | Category |
| vteCryptography |
| General | History of cryptographyOutline of cryptographyClassical cipherCryptographic protocolAuthentication protocolCryptographic primitiveCryptanalysisCryptocurrencyCryptosystemCryptographic nonceCryptovirologyHash functionCryptographic hash functionKey derivation functionSecure Hash AlgorithmsDigital signatureKleptographyKey (cryptography)Key exchangeKey generatorKey scheduleKey stretchingKeygenMachinesRansomwareRandom number generationCryptographically secure pseudorandom number generator(CSPRNG)Pseudorandom noise(PRN)Secure channelInsecure channelSubliminal channelEncryptionDecryptionEnd-to-end encryptionHarvest now, decrypt laterInformation-theoretic securityPlaintextCodetextCiphertextShared secretTrapdoor functionTrusted timestampingKey-based routingOnion routingGarlic routingKademliaMix network |
| Mathematics | Cryptographic hash functionBlock cipherStream cipherSymmetric-key algorithmAuthenticated encryptionPublic-key cryptographyQuantum key distributionQuantum cryptographyPost-quantum cryptographyMessage authentication codeRandom numbersSteganography |
| Category |

 
| vteTree data structures |
| --- |
| Search trees(dynamic sets,associative arrays) | 2–32–3–4AA(a,b)AVLBB+K-DimensionalB*BxBinary searchOptimalSelf-balancingDancingHTreeIntervalOrder statisticPalindrome(Left-leaning)Red–blackScapegoatSplayTTreapUBWeight-balanced |
| Heaps | BinaryBinomialBrodald-aryFibonacciLeftistPairingSkew binomialSkewvan Emde BoasWeak |
| Tries | CtrieC-trie(compressed ADT)HashRadixSuffixTernary searchX-fastY-fast |
| Spatialdatapartitioning trees | BallBKBSPCartesianHilbert Rk-d(implicitk-d)MMetricMVPOctreePHPriority RQuadRR+R*SegmentVPX |
| Other trees | CoverExponentialFenwickFingerFractal indexFusionHash calendariDistanceK-aryLeft-child right-siblingLink/cutLog-structured mergeMerklePQRangeSPQRTop |