# The Three Faces of OWL

OWL (Web Ontology Language) has three sublanguages, strictly ordered by expressiveness: **OWL Full > OWL DL > OWL Lite**.

## 1. OWL Full
The complete language with maximum expressiveness.
*   **Features:**
    *   Allows arbitrary combinations of OWL and RDF constructs.
    *   A class can be treated as an individual (member of another class) simultaneously.
    *   Any legal RDF document is a valid OWL Full document.
*   **Advantage:** Maximum flexibility and expressiveness.
*   **Disadvantage:** Computationally expensive; complete automated reasoning is generally undecidable (no guarantee a computer can solve every problem).

## 2. OWL DL (Description Logic)
A restricted sublanguage designed for computational completeness.
*   **Restrictions:**
    *   **Strict Separation:** A resource must be clearly defined as a class, property, or individual—it cannot be multiple things at once.
        *   *(Example: `Camera` cannot be defined as a `Class` and also used as an instance of another class simultaneously).*
    *   **Property Constraints:** Functional and Inverse Functional properties can only be used with Object Properties (not Datatype properties).
        *   *(Example: You cannot mark a Datatype property like `age` as `Functional` in OWL DL).*
    *   **Transitivity:** Cannot use cardinality constraints on transitive properties.
    *   **Imports:** Cannot import an OWL Full ontology.
*   **Advantage:** Guaranteed computational completeness (reasoners will finish and give correct answers) and better performance than OWL Full.
*   **Disadvantage:** Less flexible than OWL Full.

## 3. OWL Lite
The most restricted subset, designed for simple hierarchies and constraints.
*   **Restrictions:**
    *   **Removed Constructs:** No `owl:hasValue`, `owl:disjointWith`, `owl:unionOf`, `owl:complementOf`, or `owl:oneOf`.
        *   *(Example: You cannot use `owl:hasValue` to define a class "RedThings" that always has color "Red").*
    *   **Cardinality:** Restricted to values of **0 or 1** only. No `minCardinality` or `maxCardinality`.
        *   *(Example: Can specify "has exactly 1 ID", but cannot specify "has 4 wheels").*
    *   **Equivalence:** `owl:equivalentClass` can only be used between named classes (no anonymous classes).
*   **Advantage:** Easiest to implement tools and reasoners for; highly efficient.
*   **Disadvantage:** Lowest expressive power.

## Example Analysis
Based on the Camera Ontology discussed:
*   It uses `owl:hasValue` $\rightarrow$ Cannot be **OWL Lite**.
*   It uses a functional property on a `DatatypeProperty` $\rightarrow$ Cannot be **OWL DL**.
*   **Conclusion:** The Camera Ontology is **OWL Full**.