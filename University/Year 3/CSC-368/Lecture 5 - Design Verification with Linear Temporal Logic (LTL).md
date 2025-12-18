#### Why do we need design verification?
- Embedded systems are used in safety-critical systems a lot of the time.

#### Linear Temporal Logic (LTL):
- A formal language used to specify and verify the behaviour of systems over time.
	- LTL = propositional logic + temporal operators on traces

#### Definitions:
- Observation:
	- tr(i) = tr(i,i) = (si, xi, yi) -> basically all combinations of all inputs between steps i and i
![[Pasted image 20251217125751.png]]
^ Tr(1) = Tr(1,1) = All traces between index 1 and 1.

![[Pasted image 20251217125821.png]]
^ Tr(1,2) = All traces between index 1 and 2.

![[Pasted image 20251217125904.png]]
^ Traces 3 onwards.

#### Formula evaluation:
- Atomic formula X is true is x(i) = T
- Atomic formula Y is true if (y)i = T
- Atomic formula X=15 is true if xi(X) = 15
- Atomic formula S is true if s = s(i)
#### Formulas without nested temporal operators: 
- p is true over tr iff p is true at tr(0)
- Xp is true over tr iff p is true at tr(1) -> Note the "X" is like an "increment by 1" signal. XXp means at tr(2) for example.
- p1 U p2 is true over tr iff p1 is true at all instances until p2 is true.
- Fp is true over tr iff p is true at any tr(i)
- Gp is true over tr iff p is true at every tr, so tr(0), 1, 2, 3, ... 

#### Interesting examples:
G(Out -> y=y-1) -> For all states, if "Out" is true, y decrements by 1 from the previous state.