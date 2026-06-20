---
source: sources/wiki-ArXiv_identifier.md
source_url: https://en.wikipedia.org/wiki/ArXiv_(identifier)
---

## arXiv: Open-Access Preprint Repository for Scientific Research

arXiv is an open-access repository of electronic preprints and postprints in mathematics, physics, astronomy, electrical engineering, computer science, quantitative biology, statistics, mathematical finance, and economics. Founded in 1991 by Paul Ginsparg at Los Alamos National Laboratory and later moved to Cornell University, it is the dominant preprint distribution platform in physics and mathematics. As of November 2024, it receives approximately 24,000 submissions per month and has surpassed two million articles. In March 2026, arXiv announced it would become an independent nonprofit, separating from Cornell on July 1, 2026.

## Key Concepts

- **Preprint vs. postprint**: arXiv hosts both preprints (before peer review) and postprints (after peer review, where publishers permit). Content is moderated but **not peer reviewed**.
- **Open access pioneer**: arXiv was a precipitating factor in the broader open access movement in scientific publishing. It is a top-10 global host of green open access.
- **Self-archiving norm**: In many fields of mathematics and physics, almost all papers are self-archived on arXiv before journal publication.
- **Endorsement system** (introduced 2004): New authors in certain categories must be endorsed by an established arXiv author. Authors from recognized academic institutions typically receive automatic endorsement. Endorsers check topical appropriateness, not correctness.
- **Moderation**: Area moderators may recategorize off-topic submissions or reject non-scientific content. An automated quality-control process also screens all submissions.
- **AI-generated content policy** (November 2025): arXiv no longer accepts CS review articles and position papers that have not been vetted by a peer-reviewed journal or conference, due to a surge in AI-generated submissions. Conference workshop papers are also excluded.
- **Withdrawn preprints**: Approximately 14,000 preprints have been withdrawn, most commonly for "crucial errors."
- **Notable example of arXiv-only publication**: Grigori Perelman posted his proof of the Poincare conjecture solely on arXiv (2002), never submitting to a journal, yet was offered the Fields Medal and Clay Millennium Prize.

## Commands and Syntax

- **Paper identifier formats**:
  - Modern: `YYMM.NNNNN` (e.g., `1507.00123`) or `YYMM.NNNN` (e.g., `0704.0001`)
  - Legacy: `arch-ive/YYMMNNN` (e.g., `hep-th/9901001`)
  - Versioning: append `vN` (e.g., `1709.08980v1`); omitting defaults to latest version
- **Category system**: Hierarchical tagging — single-layer (e.g., `hep-ex` for high energy physics experiments) or two-layer (e.g., `q-fin.TR` for Trading and Market Microstructure within quantitative finance)
- **Submission formats**: LaTeX (preferred, leveraging compact TeX transmission), PDF from word processors. Submissions are rejected if PDF generation fails, images are too large, or total size exceeds limits.
- **Metadata access**: Available via OAI-PMH protocol; indexed by BASE, CORE, Unpaywall, and other aggregators
- **DOIs**: Automatically assigned to articles since January 2022, in collaboration with DataCite

## Relationships

- **Open access movement**: arXiv's success was a key catalyst for the broader shift toward open access scientific publishing
- **TeX/LaTeX ecosystem**: arXiv was made possible by the compact TeX format enabling efficient Internet transmission of scientific papers
- **Institutional funding model**: Supported by Cornell University Library, the Simons Foundation, and ~220 member institutions paying tiered annual fees ($1,000–$4,400 based on usage)
- **Preprint culture**: Established the norm of preprint sharing that later spread to other disciplines via servers like bioRxiv, medRxiv, and SSRN
- **DOI/DataCite integration**: Connects arXiv papers into the formal scholarly identifier infrastructure
- **CrossRef/Unpaywall**: Over 500,000 arXiv URLs linked as open access versions of publisher records

## Exam-Relevant Points

- arXiv was founded **August 14, 1991** by **Paul Ginsparg** at **Los Alamos National Laboratory**; moved to **Cornell University in 2001**; becoming independent nonprofit **July 1, 2026**
- Pronounced "archive" — the X represents the Greek letter chi (χ)
- Content is **moderated but not peer reviewed**
- The **endorsement system** (2004) requires new authors to be endorsed by established contributors; institutional authors are auto-endorsed
- Paper IDs follow `YYMM.NNNNN` format with version suffixes; legacy format is `archive/YYMMNNN`
- **Copyright varies per paper**: public domain, Creative Commons (CC BY-SA 4.0 or CC BY-NC-SA 4.0), publisher-copyrighted with author distribution rights, or author-copyrighted with non-exclusive license to arXiv
- Metadata is exposed via **OAI-PMH**, the standard protocol for open access repositories
- Named one of "10 computer codes that transformed science" by *Nature* (January 2021)
- As of late 2024: **~24,000 submissions/month**, **2+ million total articles**
- November 2025 policy change: CS review articles and position papers now require prior peer-reviewed acceptance due to AI-generated content concerns
