#### What is an Embedded System?
- Electronic system where software and hardware has been integrated to perform a specific function

#### Features of an embedded system: SAPDA
- Sensors
	- Intended to capture physical data from the environment
	- Generates signals which can be used as input for system
- Analog 2 Digital
	- Converts analog signal to a digital one
- Processing Unit (Has Software and Memory)
	- Does all the processing and shit
- Digital 2 Analog
	- Converts digital signal to an analog one
- Actuators
	- Uses signals, interacts with and alters the physical environment

#### A system block diagram:
- Visually represents connections and relationships between inputs, outputs and subsystems.
- X1, X2, ... are the inputs
- Y is the **SET** of outputs
- S is the system which may be built up of subsystems.
![[Pasted image 20251218112452.png]]
Y as an output can be considered as an output of the function S applied to inputs.
**Y = S(x1, x2, ... xn)**

#### Signals: 
- A time varying voltage, current or EM wave that carries information
- Can be obtained from sensors to be used as inputs
- Can be produced from a system as outputs

#### Discrete Signals:
- Signals in which the times they are present can be counted
	- i.e. stored as an integer
- A discrete system is a system which operates on these discrete values

#### An FSM Visualised: 
![[Pasted image 20251218112821.png]]
Transitions have the following format:
**X / Y  where: **
- X are the guards
	- Constraints that must be satisfied to take the action, think of them like an "if" statement
- Y are the actions / side effects
	- Changes that happen to the system as the transition is happening,  think of them like the body of an "if" statement.

#### Parallel decomposition
![[Pasted image 20251218113046.png]]
- There is a superstate "PowerOn" which contains 2 systems:
	- Fan1
	- Fan 2
- These fan systems will operate based on the same input, if we are in the PowerOn superstate.
- If constraints of a given transition is satisfied in both systems, both will transition
	- If only one, only one will transition
	- if none, none transition
- The lack of a history junction (h) means once you leave PowerOn, states go back to wherever they start next time you enter.

#### Linear Temporal Logic - LTL
- p is true over tr iff p is true at Tr(0)
- Xp is true over tr iff p is true at Tr(1)
- P1 U P2 is true iff p2 is true at some point, and p1 is true all the time until then
- Fp is true over tr iff  p is true at any point
- Gp is true over tr iff p is true in all traces tr(0) to tr(inf)

#### Nesting LTL formulae: 
- Xf is true iff f is true over tr(1,inf) -> aka drop the first trace / move over by 1
- f1 U f2 is true over tr iff f2 is true at some point i , and f1 is true in all subsets of traces that start before i and end at inf
-  Ff is true if f is true at some point
- Gf is true if f is true in all subsystems from tr(0, inf) to tr(inf-1, inf) -> make sure they all go to the end of the table however!

#### Signal Temporal Logic Syntax:
- f U[a,b] y
	- f will keep holding until y holds, at some point between a and b
- F[a,b] f
	- f will eventually hold at some point between a and b
- G[a,b]f
	- f always holds, at all times, between a and b

#### How to evaluate a wave with signal temporal logic syntax?
- Do it in increments of 0.5
	- If 1.5 satisfies, ensure 1-2 are all "up"


#### Open Loop Control Systems: 
- No feedback
- Often the sequencing of events by on/off signals

#### Closed Loop Control Systems
- Has feedback
- Error -> The difference between required value and actual value
- Positive feedback -> Add feedback to input
	- G(overall) = y/x = G/(1-GH)
- Negative feedback -> Subtract feedback from input 
	- G(overall) = y/x = G/(1+GH)
- For transfer functions, just slap an (S) after every letter

#### PID Control:
- Proportional (Magnitude at a given point)
- Integral (Integration)
	- Space under curve
- Derivative (Differentiation)
	- Gradient at a given time

