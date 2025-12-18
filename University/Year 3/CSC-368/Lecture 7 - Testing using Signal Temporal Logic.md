#### A Signal:
- Any time-varying voltage, current or EM wave which carries information
- Can be obtained from sensors to be used as inputs.
- Can be produced by a system as outputs.

#### A discrete signal:
- A signal is discrete when the number of times it is present can be counted (or represented as an integer)
- A discrete system is a system which operates on discrete values.

#### Signal Temporal Logic Syntax (a,b) can be considered the scope:  
- X U[a,b] Y -> X will keep holding until Y holds some time between a and b 
- F[a,b]Y -> Y will eventually hold sometime between a and b
- G[a,b] Y -> Y will hold at all times between a and b 

#### How do you evaluate these STL syntax on a real time signal? 
- p(X) -> True if the predicate is true at the index of which is being assigned.
![[Pasted image 20251217132308.png]]
![[Pasted image 20251217132359.png]]

#### The following one is a little more challenging. Consider it in steps of 0.5 and it should be easier, then spread that out to 1sq wide and youre coolin! 
![[Pasted image 20251217132829.png]]
![[Pasted image 20251217132926.png]]

#### For more complex formulae, consider it like a tree in which you can split it into its independent components and create signals for them individually and then build your way back up the tree.