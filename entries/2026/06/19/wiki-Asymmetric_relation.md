---
source: sources/wiki-Asymmetric_relation.md
source_url: https://en.wikipedia.org/wiki/Asymmetric_relation
---

## Asymmetric Relations in Binary Relation Theory

This page defines asymmetric relations — binary relations where if *a* is related to *b*, then *b* is never related to *a*. It provides the formal definition, equivalent characterizations, examples and non-examples, sufficient conditions for asymmetry, and situates asymmetric relations within the broader taxonomy of transitive binary relations (partial orders, total orders, strict orders, equivalence relations, etc.).

## Key Concepts

- **Asymmetric relation**: A binary relation R on a set X where for all a, b in X, if aRb then not bRa. Equivalently: for all a, b in X, it is never the case that both aRb and bRa hold.
- **Equivalent characterization**: A relation is asymmetric if and only if it is both **antisymmetric** and **irreflexive**. This is both necessary and sufficient.
- **Asymmetry implies irreflexivity**: If R is asymmetric, then no element can be related to itself (since aRa would require not aRa).
- **Asymmetry vs. "not symmetric"**: These are distinct properties. The relation <= is neither symmetric nor asymmetric. A relation can be non-symmetric without being asymmetric.
- **The empty relation** is the only relation that is both symmetric and asymmetric (vacuously).
- **Closure properties**: Restrictions and converses of asymmetric relations are also asymmetric.
- **Connex complement**: A relation is connex if and only if its complement is asymmetric.
- **Not all asymmetric relations are transitive**: Rock-paper-scissors is asymmetric but antitransitive (not even transitive).

## Commands and Syntax

No commands per se, but key formal notation:

- **Definition in first-order logic**: `forall a,b in X: aRb => not(bRa)`
- **Equivalent formulation**: `forall a,b in X: not(aRb and bRa)`
- **Binary relation notation**: aRb is shorthand for (a, b) in R, where R is a subset of X x X.

## Relationships

- **Antisymmetric + Irreflexive = Asymmetric**: Asymmetry decomposes exactly into these two properties.
- **Strict partial order**: Every strict partial order (irreflexive + transitive) is asymmetric. Asymmetry is the defining characteristic of "strict" orders vs. non-strict ones.
- **Strict total order**: Adds the connex property to a strict partial order; still asymmetric.
- **Partial order (non-strict)**: Reflexive + antisymmetric + transitive — *not* asymmetric because it is reflexive.
- **Transitive relation**: A transitive relation is asymmetric iff it is irreflexive (proof: aRb and bRa would give aRa by transitivity, contradicting irreflexivity).
- **Connex relation**: A relation's complement is asymmetric iff the relation is connex. Asymmetric relations need not be connex (e.g., strict subset).
- **Antitransitive relations**: Can be asymmetric (e.g., rock-paper-scissors), showing asymmetry is independent of transitivity.
- **Taxonomy table**: The source includes a comprehensive classification table showing which properties (symmetric, antisymmetric, connected, well-founded, reflexive, irreflexive, asymmetric) hold for equivalence relations, preorders, partial orders, total orders, well-orderings, lattices, strict partial orders, strict weak orders, and strict total orders.

## Exam-Relevant Points

- **Asymmetric = antisymmetric + irreflexive** — this equivalence is the single most testable fact. Know it in both directions.
- **Strict orders are asymmetric; non-strict orders are not.** The < relation is asymmetric; the <= relation is not.
- **For transitive relations, asymmetry and irreflexivity are equivalent.** If you know a relation is transitive, you only need to check irreflexivity to conclude asymmetry (and vice versa).
- **Asymmetric does not mean "not symmetric."** The <= relation is neither symmetric nor asymmetric. Only the empty relation is both.
- **Asymmetry implies irreflexivity** (an element can never be related to itself under an asymmetric relation).
- **Restrictions and converses preserve asymmetry** — if < is asymmetric on the reals, it is also asymmetric on any subset, and > is also asymmetric.
- **Rock-paper-scissors** is a canonical example of an asymmetric relation that is *not* a strict partial order (it fails transitivity / is antitransitive).
- **Sufficient conditions for asymmetry** (beyond the necessary antisymmetric + irreflexive): irreflexive + transitive; antitransitive + antisymmetric; antitransitive + transitive (which forces the relation to be empty or very constrained).
