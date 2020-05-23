# A Dependently-Typed Linear π-Calculus in Agda

DLπ is an Agda formalization of the **linear π-calculus** with
**dependent pairs**. It allows for the modeling of structured
conversations in which processes and types depend on the content of
exchanged messages.

## DLPi

This folder contains the full formalization of DLπ. Below is an
outline of the files and of their purpose. While looking at the
code, use of [Fira Code](https://github.com/tonsky/FiraCode) is
recommended as it contains several ligatures that make the Agda code
much more pleasant to read.

### Primary modules

* [Multiplicity.agda](DLPi/Multiplicity.agda) Representation of
  **multiplicities** and their properties, including `MScale` and
  `MSplit`.
* [Type.agda](DLPi/Type.agda) Definition of DLπ **types** and their
  properties, including `TNull`, `TScale` and `TSplit`.
* [Context.agda](DLPi/Context.agda) Definition of **contexts** and
  related properties, including `CNull`, `CScale` and `CSplit`.
* [Syntax.agda](DLPi/Syntax.agda) Data types for representing
  **terms** and **processes**. Look no further if you're looking for
  `Name`, `Term` and `Process`.
* [Semantics.agda](DLPi/Semantics.agda) The **operational
  semantics** of DLπ, including structural pre-congruence and
  labelled reduction. Both definitions embed the property that they
  preserve typing.

### Auxiliary modules

* [Common.agda](DLPi/Common.agda) Some general purpose functions,
  properties and axioms (extensionality). These are very likely to
  be found somewhere in the standard library, but so far we've been
  too lazy to look them up.
* [HasType.agda](DLPi/HasType.agda) Proof that a name not occurring
  in a well-typed process has a type that satisfies `TNull`, hence
  it is unrestricted.
* [Main.agda](DLPi/Main.agda) Container for a few **examples**, but
  mostly useful as root file that triggers the type checking of
  everything.
* [PrefixNormalForm.agda](DLPi/PrefixNormalForm.agda) Proof that
  every process can be rewritten in prefix-normal-form using
  structural pre-congruence.
* [PrefixedBy.agda](DLPi/PrefixedBy.agda) Predicate that holds when
  a process has an unguarded input/output prefix for a given channel.
* [ReducibleNormalForm.agda](DLPi/ReducibleNormalForm.agda) Proof
  that every process with both an input and an output prefix for a
  given channel can be rewritten in reducible normal form using
  structural pre-congruence. In this normal form, the two prefixes
  sit next to each other, so the process is ready to reduce.
* [Substitution.agda](DLPi/Substitution.agda) **Substitution** of
  terms for variables in processes.
* [Swapping.agda](DLPi/Swapping.agda) Some auxiliary properties
  about swapping names in a context.
* [Weakening.agda](DLPi/Weakening.agda) Definition of `Weaken` and
  weakening properties for terms and processes.

## SessionTypes

This folder contains **encoding** functions from (dependent) session
type languages to DLπ types. The folder is organized as follows:

* [Common.agda](SessionTypes/Common.agda) imports the extensionality
  principle and defines the `Type` data type for representing
  **finite DLπ types**.
* [FinLabels](SessionTypes/FinLabels) contains the encoding of
  non-dependent, labeled session types with n-ary branches and
  choices. Labels are elements of the `Fin n` data type.
* [LinearLogic](SessionTypes/LinearLogic) contains the encoding of
  dependent session types *à la* [Toninho, Caires & Pfenning
  2011](https://doi.org/10.1145/2003476.2003499). These session
  types subsume the original non-dependent ones by
  [Honda](https://doi.org/10.1007/3-540-57208-2_35).
* [LabelDependent](SessionTypes/LabelDependent) contains the
  encoding of label-dependent session types defined by [Thiemann &
  Vasconcelos 2020](https://doi.org/10.1145/3371135).

Each subfolder is organized as follows:

* `Types.agda` defines **session types** and auxiliary data types,
  including the notion of bisimilarity used for proving that
  decoding is the inverse of encoding.
* `Encoding.agda` defines a predicate on `Type` that characterizes
  the image of the encoding.
* `Encode.agda` defines the **encoding** function and proves that it
  satisfies the `Encoding` predicate.
* `Decode.agda` defines the **decoding** function.
* `Proofs.agda` contains the proofs that encoding and decoding are
  one the **inverse** of the other modulo bisimilarity.
* `Equalities.agda`, if present, contains examples illustrating
  the fact that the encoding function is **not injective**.
