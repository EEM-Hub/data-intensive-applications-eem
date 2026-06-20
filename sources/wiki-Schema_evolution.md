---
source: https://en.wikipedia.org/wiki/Schema_evolution
fetched: 2026-06-19
---

Altering a data schema while preserving data 
|  | This article'stone or style may not reflect theencyclopedic toneused on Wikipedia.See Wikipedia'sguide to writing better articlesfor suggestions.(January 2026)(Learn how and when to remove this message) |
| --- | --- |

 

In [computer science](./Computer_science), **schema versioning** and **schema evolution**, deal with the need to retain current data and [software system](./Software_system) functionality in the face of changing database structure.[[1]](./Schema_evolution#cite_note-1)  The problem is not limited to the modification of the schema. It, in fact, affects the data stored under the given schema and the queries (and thus the applications) posed on that schema.

 

A database design is sometimes created as a "as of now" instance and thus schema evolution is not considered. (This is different but related to where a database is designed as a "one size fits all" which doesn't cover attribute volatility). This assumption, almost unrealistic in the context of traditional [information systems](./Information_systems), becomes unacceptable in the context of systems that retain large volumes of historical information or those such as web information systems, that due to the [distributed](./Distributed_computing) and cooperative nature of their development, are subject of an even stronger pressure toward change (from 39% to over 500% more intense than in traditional settings).[[2]](./Schema_evolution#cite_note-2) Due to this historical heritage the process of schema evolution as of 2008 a particularly taxing one. It is, in fact, widely acknowledged that the data management core of an applications is one of the most difficult and critical components to evolve. The key problem is the impact
of the schema evolution on queries and applications. As shown in the article *Schema Evolution in Wikipedia - Toward a Web Information System Benchmark* (2008)[[3]](./Schema_evolution#cite_note-curino-iceis2008-3) (which provides an analysis of the [MediaWiki](./MediaWiki) evolution) each evolution step might affect up to 70% of the queries operating on the schema, that must be manually reworked consequently.

 

In 2008, the problem has been recognized as a pressing one by the database community for more than 12 years.[[4]](./Schema_evolution#cite_note-4)[[5]](./Schema_evolution#cite_note-5) Supporting schema evolution is a difficult problem involving complex mapping among schema versions and the tool support has been so far very limited. The recent theoretical advances on mapping composition[[6]](./Schema_evolution#cite_note-6) and mapping invertibility,[[7]](./Schema_evolution#cite_note-7) which represent the core problems underlying the schema evolution remains almost inaccessible to the large public.[*[why?](./Wikipedia:Please_clarify)*] The issue is particular felt by [temporal databases](./Temporal_database).[[8]](./Schema_evolution#cite_note-8)

 

## Related works

 
- A rich bibliography on Schema Evolution is collected at: [http://se-pubs.dbs.uni-leipzig.de/pubs/results/taxonomy%3A100](http://se-pubs.dbs.uni-leipzig.de/pubs/results/taxonomy%3A100)
- UCLA university carried out an analysis of the MediaWiki Schema Evolution: [Schema Evolution Benchmark](http://yellowstone.cs.ucla.edu/schema-evolution/index.php/Schema_Evolution_Benchmark)
- PRISM, a tool to support graceful relational schema evolution: [Prism: schema evolution tool](http://yellowstone.cs.ucla.edu/schema-evolution/index.php/Schema_Evolution_Tool)
- PRIMA, a tool supporting [transaction time](./Transaction_time) databases under schema evolution [PRIMA: supporting transaction-time DB under schema evolution](http://prima.schemaevolution.org)
- [Pario](./Pario?action=edit&redlink=1) and deltasql[[9]](./Schema_evolution#cite_note-9) are examples of software development tools that include fully automated schema evolution.

 

## References

 
1. [↑](./Schema_evolution#cite_ref-1) Roddick, John F (1995). "A survey of schema versioning issues for database systems". *Information and Software Technology*. **37** (7): 383–393. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.54.8474](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.54.8474). [doi](./Doi_(identifier)):[10.1016/0950-5849(95)91494-K](https://doi.org/10.1016%2F0950-5849%2895%2991494-K).
2. [↑](./Schema_evolution#cite_ref-2) ["Schema Evolution Benchmark - Schema Evolution"](http://yellowstone.cs.ucla.edu/schema-evolution/index.php/Schema_Evolution_Benchmark). yellowstone.cs.ucla.edu. Retrieved 2010-07-29.
3. [↑](./Schema_evolution#cite_ref-curino-iceis2008_3-0) Curino CA, Moon HJ, Tanca L, Zaniolo C (2008). [*Schema Evolution in Wikipedia: toward a Web Information System Benchmark*](http://web.cs.ucla.edu/~zaniolo/papers/ICEIS2008.pdf) (PDF). *ICEIS*.
4. [↑](./Schema_evolution#cite_ref-4) Rahm E, Bernstein PA. ["An Online Bibliography on Schema Evolution"](https://web.archive.org/web/20080512093153/http://www.sigmod.org/sigmod/record/issues/0612/p30-article-rahm.pdf) (PDF). Archived from [the original](http://www.sigmod.org/sigmod/record/issues/0612/p30-article-rahm.pdf) (PDF) on 12 May 2008. Retrieved 2 May 2017.
5. [↑](./Schema_evolution#cite_ref-5) Topor, Rodney; Salem, Kenneth; Gupta, Amarnath; Goda, Kazuo; Gehrke, Johannes; Palmer, Nathaniel; Sharaf, Mohamed; Labrinidis, Alexandros; Roddick, John F.; Fuxman, Ariel; Miller, Renée J.; Tan, Wang-Chiew; Kementsietsidis, Anastasios; Bonnet, Philippe; Shasha, Dennis; Roddick, John F.; Gupta, Amarnath; Peikert, Ronald; Ludäscher, Bertram; Bowers, Shawn; McPhillips, Timothy; Naumann, Harald; Voruganti, Kaladhar; Domingo-Ferrer, Josep; Carterette, Ben; Ipeirotis, Panagiotis G.; Arenas, Marcelo; Manolopoulos, Yannis; Theodoridis, Yannis; et al. (2009). "Schema Versioning". *Encyclopedia of Database Systems*. Springer, Boston, MA. pp. 2499–2502. [doi](./Doi_(identifier)):[10.1007/978-0-387-39940-9_323](https://doi.org/10.1007%2F978-0-387-39940-9_323). [ISBN](./ISBN_(identifier)) [978-0-387-35544-3](./Special:BookSources/978-0-387-35544-3).
6. [↑](./Schema_evolution#cite_ref-6) Nash, Alan; Bernstein, Philip A.; Melnik, Sergey (2007). "Composition of mappings given by embedded dependencies". *ACM Transactions on Database Systems*. **32**: 4–es. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.534.3957](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.534.3957). [doi](./Doi_(identifier)):[10.1145/1206049.1206053](https://doi.org/10.1145%2F1206049.1206053).
7. [↑](./Schema_evolution#cite_ref-7) Fagin R, Kolaitis PG, Popa L, Tan WC. ["Quasi-inverses of Schema Mappings"](http://www.almaden.ibm.com/cs/people/fagin/quasi.pdf) (PDF).
8. [↑](./Schema_evolution#cite_ref-8) Roddick, John F.; Snodgrass, Richard T. (1995). "Schema Versioning". *The TSQL2 Temporal Query Language*. The Springer International Series in Engineering and Computer Science. Springer, Boston, MA. pp. 427–449. [doi](./Doi_(identifier)):[10.1007/978-1-4615-2289-8_22](https://doi.org/10.1007%2F978-1-4615-2289-8_22). [ISBN](./ISBN_(identifier)) [9781461359661](./Special:BookSources/9781461359661).
9. [↑](./Schema_evolution#cite_ref-9) ["deltasql, Database Evolution Under Control"](http://deltasql.sourceforge.net). Deltasql Development Team. 2013-04-20. Retrieved 2019-02-08.

 
|  | Thiscomputer sciencearticle is astub. You can help Wikipedia byadding missing information. |
| --- | --- |

- [v](./Template:Comp-sci-stub)
- [t](./Template_talk:Comp-sci-stub)
- [e](./Special:EditPage/Template:Comp-sci-stub)