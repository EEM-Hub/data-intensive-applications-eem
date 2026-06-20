---
source: https://en.wikipedia.org/wiki/Virtual_node
fetched: 2026-06-19
---

Device or point within a network capable of creating, receiving, or transmitting data This article is about a point within a telecommunications network. For other uses, see [Node (disambiguation)](./Node_(disambiguation)). 

In [networking](./Computer_network), a **node** ([Latin](./Latin_language): *nodus*, 'knot') is either a redistribution point or a [communication endpoint](./Communication_endpoint) within [telecommunication networks](./Telecommunication_network) or [computer networks](./Computer_network). 

 

A physical network node is an electronic device that is attached to a network, and is capable of creating, receiving, or transmitting information over a [communication channel](./Communication_channel).[[1]](./Node_(networking)#cite_note-1) In data communication, a physical network node may either be [data communication equipment](./Data_communication_equipment) (such as a [modem](./Modem), [hub](./Network_hub), [bridge](./Network_bridge) or [switch](./Network_switch)) or [data terminal equipment](./Data_terminal_equipment) (such as a digital telephone handset, a printer or a [host computer](./Host_computer)). 

 

A [passive](./Passivity_(engineering)) distribution point, such as a [distribution frame](./Distribution_frame) or [patch panel](./Patch_panel) is not considered to be a node.

 

## Computer networks

 

In data communication, a physical network node may either be [data communication equipment](./Data_communication_equipment) (DCE) such as a [modem](./Modem), [hub](./Network_hub), [bridge](./Network_bridge) or [switch](./Network_switch); or [data terminal equipment](./Data_terminal_equipment) (DTE) such as a digital telephone handset, a printer or a [host computer](./Host_computer).

 

If a network is a [local area network](./Local_area_network) (LAN) or [wide area network](./Wide_area_network) (WAN), every LAN or WAN node that participates on the [data link layer](./Data_link_layer) must have a [network address](./Network_address), typically one for each [network interface controller](./Network_interface_controller) it possesses. Examples are computers, a [DSL modem](./DSL_modem) with Ethernet interface and [wireless access point](./Wireless_access_point). Equipment, such as an [Ethernet hub](./Ethernet_hub) or modem with [serial interface](./Serial_interface), that operates only below the data link layer does not require a network address.[[2]](./Node_(networking)#cite_note-2)

 

If the network in question is the [Internet](./Internet) or an [intranet](./Intranet), many physical network nodes are host computers, also known as *Internet nodes*, identified by an [IP address](./IP_address), and all hosts are physical network nodes. However, some data-link-layer devices such as switches, bridges and wireless access points do not have an IP host address (except sometimes for administrative purposes), and are not considered to be Internet nodes or hosts, but are considered physical network nodes and LAN nodes.

 

## Telecommunications

 

In the fixed telephone network, a node may be a public or private [telephone exchange](./Telephone_exchange), a [remote concentrator](./Remote_concentrator) or a computer providing some [intelligent network service](./Intelligent_network_service). In cellular communication, switching points and databases such as the [base station controller](./Base_station_controller), [home location register](./Home_location_register), [gateway GPRS Support Node](./Gateway_GPRS_Support_Node) (GGSN) and [serving GPRS support node](./Serving_GPRS_support_node) (SGSN) are examples of nodes. Cellular network [base stations](./Base_station) are not considered to be nodes in this context.

 

In [cable television](./Cable_television) systems (CATV), this term has assumed a broader context and is generally associated with a [fiber optic](./Fiber-optic_communication) node. This can be defined as those homes or businesses within a specific geographic area that are served from a common fiber optic [receiver](./Receiver_(information_theory)). A fiber optic node is generally described in terms of the number of *homes passed* that are served by that specific fiber node.

 

## Distributed systems

 

In a [distributed system](./Distributed_system) network, the nodes are [clients](./Client_(computing)), [servers](./Server_(computing)) or [peers](./Peer_(networking)). A peer may sometimes serve as client, sometimes server. In a [peer-to-peer](./Peer-to-peer) or [overlay network](./Overlay_network), nodes that actively route data for the other networked devices as well as themselves are called [supernodes](./Supernode_(networking)).

 

Distributed systems may sometimes use *virtual nodes* so that the system is not oblivious to the heterogeneity of the nodes. This issue is addressed with special algorithms, like [consistent hashing](./Consistent_hashing), as it is the case in [Amazon's Dynamo](./Dynamo_(storage_system)).[[3]](./Node_(networking)#cite_note-3)

 

Within a vast computer network, the individual computers on the periphery of the network, those that do not also connect other networks, and those that often connect transiently to one or more [clouds](./Cloud_computing) are called end nodes. Typically, within the cloud computing construct, the individual user or customer computer that connects into one well-managed cloud is called an end node. Since these computers are a part of the network yet unmanaged by the cloud's host, they present significant risks to the entire cloud. This is called the [end node problem](./End_node_problem).[[4]](./Node_(networking)#cite_note-4) There are several means to remedy this problem but all require instilling trust in the end node computer.[[5]](./Node_(networking)#cite_note-5)

 

## See also

 
- [End system](./End_system)
- [Middlebox](./Middlebox)
- [Networking hardware](./Networking_hardware)
- [Terminal (telecommunication)](./Terminal_(telecommunication))

 

## References

  
1. [↑](./Node_(networking)#cite_ref-1) ["Node"](https://web.archive.org/web/20090213103406/http://encarta.msn.com/encnet/features/dictionary/DictionaryResults.aspx?refid=1861633439). *Encarta*. [Microsoft](./Microsoft). Archived from [the original](https://encarta.msn.com/encnet/features/dictionary/DictionaryResults.aspx?refid=1861633439) on 2009-02-13. Retrieved 2007-10-23.
2. [↑](./Node_(networking)#cite_ref-2) ["Networking-a-complete-guide"](https://www.ibm.com/cloud/learn/networking-a-complete-guide). *[IBM](./IBM)*.
3. [↑](./Node_(networking)#cite_ref-3) ["Dynamo: Amazon's Highly Available Key-value Store: 4.2 Partitioning Algorithm"](http://www.allthingsdistributed.com/files/amazon-dynamo-sosp2007.pdf) (PDF). *www.allthingsdistributed.com*. All things distributed. Retrieved 2011-03-17. the basic algorithm is oblivious to the heterogeneity in the performance of nodes. To address these issues, Dynamo uses a variant of consistent hashing: instead of mapping a node to a single point in the circle, each node gets assigned to multiple points in the ring. To this end, Dynamo uses the concept of "virtual nodes". A virtual node looks like a single node in the system, but each node can be responsible for more than one virtual node. Effectively, when a new node is added to the system, it is assigned multiple positions (henceforth, "tokens") in the ring.
4. [↑](./Node_(networking)#cite_ref-4) David D. Clark (April 2009), [*Architecture from the top down*](https://web.archive.org/web/20210813140541/http://www.nets-find.net/Meetings/S09Meeting/Talks/clark.ppt), archived from [the original](http://www.nets-find.net/Meetings/S09Meeting/Talks/clark.ppt) on 2021-08-13, retrieved 2017-05-14
5. [↑](./Node_(networking)#cite_ref-5) ["LPS-Public"](https://web.archive.org/web/20110129060950/http://www.spi.dod.mil/lipose.htm). Archived from [the original](http://www.spi.dod.mil/lipose.htm) on 2011-01-29.

 
| vteTelecommunications |
| --- |
| History | BeaconBroadcastingCable protection systemCable TVCommunications satelliteComputer networkData compressionaudioDCTimagevideoDigital mediaInternet videoonline video platformsocial mediastreamingDrumsEdholm's lawElectrical telegraphFaxHeliographsHydraulic telegraphInformation AgeInformation revolutionInternetMass mediaMobile phoneSmartphoneOptical telecommunicationOptical telegraphyPagerPhotophonePrepaid mobile phoneRadioRadiotelephoneSatellite communicationsSemaphorePhryctoriaSemiconductordeviceMOSFETtransistorSmoke signalsTelecommunications historyTelautographTelegraphyTeleprinter(teletype)TelephonehistoryThe Telephone CasesTelevisiondigitalstreamingUndersea telegraph lineVideotelephonyWhistled languageWireless revolution |
| Pioneers | Nasir AhmedEdwin Howard ArmstrongMohamed M. AtallaJohn Logie BairdPaul BaranJohn BardeenAlexander Graham BellEmile BerlinerTim Berners-LeeFrancis BlakeJagadish Chandra BoseCharles BourseulWalter Houser BrattainVint CerfClaude ChappeYogen DalalDonald DaviesDaniel Davis Jr.Amos DolbearThomas EdisonPhilo FarnsworthReginald FessendenLee de ForestElisha GrayOliver HeavisideRobert HookeErna Schneider HooverHarold HopkinsGardiner Greene HubbardBob KahnDawon KahngCharles K. KaoNarinder Singh KapanyHedy LamarrRoberto LandellInnocenzo ManzettiGuglielmo MarconiRobert MetcalfeAntonio MeucciSamuel MorseJun-ichi NishizawaCharles Grafton PageRadia PerlmanAlexander Stepanovich PopovTivadar PuskásJohann Philipp ReisClaude ShannonAlmon Brown StrowgerHenry SuttonCharles Sumner TainterNikola TeslaCamille TissotAlfred VailThomas A. WatsonCharles WheatstoneVladimir K. ZworykinInternet pioneers |
| Transmissionmedia | Coaxial cableFiber-optic communicationoptical fiberFree-space optical communicationMolecular communicationRadio waveswirelessTransmission linetelecommunication circuit |
| Network topologyand switching | BandwidthLinksNetwork switchingcircuitpacketNodesterminalTelephone exchange |
| Multiplexing | Space-divisionFrequency-divisionTime-divisionPolarization-divisionOrbital angular-momentumCode-division |
| Concepts | Communication protocolComputer networkData transmissionStore and forwardTelecommunications equipment |
| Types of network | Cellular networkEthernetISDNLANMobileNGNPublic Switched TelephoneRadioTelevisionTelexUUCPWANWireless network |
| Notable networks | ARPANETBITNETCYCLADESFidoNetInternetInternet2JANETNPL networkTANetToasternetUsenet |
| Locations | AfricaAmericasNorthSouthAntarcticaAsiaEuropeOceaniaGlobal telecommunications regulation bodies |
| TelecommunicationportalCategoryOutlineCommons |