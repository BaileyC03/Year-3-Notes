#### Superstates: 
- Can be considered like a bracket in mathematics. If states a,b,c,... have an "f" transition to F - instead of putting a ton of F transitions from every state to F, you can put them in a superstate and have one transition from the superstate to F. 
![[Pasted image 20251217123735.png]]
(Note that it will always go back to A in this case as it is not a history junction. AKA it wont recall the state within the superstate once you leave it)
- States will have their membership of a given superstate mentioned in the trace table: 
 ![[Pasted image 20251217124100.png]]
-  S,A means "A in the superstate S" I think?


#### History Junctions:
- Having a little "H" in a circle in the superstate implies that the superstate has a history junction. This means that once you leave the state, the position in which the superstate was in is preserved. i.e. if you are in state "B" and make an "f" then a "g" transition, you return to state B.
![[Pasted image 20251217124254.png]]

#### Parallel Decomposition:
- If a superstate contains two systems in it, they will both be running **AT THE SAME TIME** and listening for inputs and.  
- If both subsystems have a transition on action "a" or both have their guard satisfied, they will both transition in any given step..
- If only one does, only that one will transition whereas the other will stay where it is. 
![[Pasted image 20251217124608.png]]
