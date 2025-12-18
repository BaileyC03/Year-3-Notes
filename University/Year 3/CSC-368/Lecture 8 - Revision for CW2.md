#### System Block Diagram:
![[Pasted image 20251217133544.png]]
X1, X2 -> Inputs
Y -> Set of outputs
S -> System.


#### LTL Formula Evaluation
1. P is true over tr iff p is true at tr0
2. XP is true over tr iff p is true at tr(1)
3. P1 U P2 is true if P2 is true at some point and P1 is true up until that.
4. FP is true if P is true ever at any point
5. GP is true if P is true at ALL points in all tr values.

#### Nested LTL Formulae
- Xn is true if n is true over tr(1,inf) -> aka you increment the whole scope by 1
- n1 U n2 is true if n2 is true at some point and n1 is true at all points until then.
- Fn is true if n is true at some point tr(i, inf)
- Gn is true if n is true over all starting points to inf.

#### Signal Temporal Logic
- A U[a,b] B -> A will keep holding until B holds at some point within the scope [a to b]
- F[a,b] A -> A will eventually hold at some point within the scope [a to b]
- G[a,b]A -> A will hold at ALL POINT within the scope [a to b]
- 