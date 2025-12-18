#### What is an embedded system?
- A system where software and hardware have been integrated to perform a specific structure
- A robot, for example, is a **composition** of integrated systems.
-  It shouldnt be able to be reprogrammed in order for it to be an integrated system

#### Embedded system structure:
- Sensor (Obtains information from the environment and produces a signal)
- Analog to Digital conversion
- Processing Unit (Contains software and memory)
- Digital to Analog conversion
- Actuators (Obtains signals and interacts with the environment accordingly)
![[Pasted image 20251217111144.png]]

#### System block diagrams: 
- A visual representation of the connections and relationships between inputs, outputs and subsystems.
![[Pasted image 20251217111341.png]]
- X1 and X2 are inputs.
- Y is the **set** of outputs.
- S is the system, it may be composed of subsystems
- The function of this system block can be considered as Y = S(x1, x2)
	- Y is the result of applying function S to x1 and x2.

#### Sensors: 
- A device that captures physical data from the physical environment
- They generate signals which can be used as inputs for a system.
- E.G: 
	- Pressure sensors
	- Motion sensors
	- Temperature sensors etc...

#### Actuators:
- A device which is intended to interact and alter the physical environment in some way
- They take signals in from the system.
- E.G:
	- Speakers
	- Motors 
	- Pumps

#### Signal:
- Any time-varying voltage, current or wave.
	- must carry information
- Signals can be obtained from sensors to be used as inputs
- Signals can be produced by the system as outputs. 

#### Discrete Signals: 
- A signal is discrete if the instances in which it is present can be counted (i.e. an integer amount of times)
- A **discrete system** is a system which operates on discrete values

#### Finite State Machines (FSM)
- A behaviour model of a discrete system.
- It executes transitions and generates outputs based on the provided input and current state that the system is in.
![[Pasted image 20251217112544.png]]
^ Note: The arrow from nowhere implies our starting state.
- Guard:
	- The requirement for the transition to take place
- Action:
	- A side effect of the transition taking place
- State 
	- A configuration of all variables, etc... basically the "way" in which the system exists.

#### Mathematical Notation for a FSM: 
FSM = (States, Val(in), Val(out), T, Sinit)
- States - the finite set of all states.
- Val(in) - The input values the machine accepts
- Val(out) - The output values the machine produces
- T - The set of all transition functions
- Sinit - The initial state. 

#### What is a guard? 
- A guard is a condition or boolean expression that must be evaluated to true in order for the transition to occur.
- Guards are predicates, and thus can be of any of the following forms: 
	-  P
	- X > Y
	- ¬P
	- P1 ^ P2
	- P1 v P2 
- Where p is a pure input signal (i.e. something exists or can be considered as a predicate)
- X is non-pure input signal (i.e. a number or some variable)

#### What is an action? 
- A specific operation or task which is in response to an event or condition in which the FSM transitions to another. Also can be considered a side effect. Can be: 
	- Empty (i.e. do nothing)
	- A pure output signal (i.e. something is now evaluated to true?)
	- A non pure output signal 

#### LOOK AT THIS PEOPLE COUNTER! 
![[Pasted image 20251217115006.png]]
- It only counts to two but you can see
	- I is an input meaning "person goes in"
	- O is an input meaning "person goes out"
	- Y is an output meaning "the number of people in the room"
- If I = 1, it transitions to another state and does no action (nothing after the "/")
- If o = 1, it transitions to the previous state and does on action (nothign after the "/")

#### Extended FSMs: 
- A variant of a FSM with the addition of memory! You can have variables now boy!!
- The output of an extended FSM depends on the current state, current input AND variable values!
![[Pasted image 20251217115728.png]]
- Looking at one of the transitions
	- if I = 1 (i.e. if someone enters)
		- y increments by one
		- return to the counter state
- This allows you to handle infinite people within the room with only one state as the variable y can increment infinitely and is handled in the action now instead of the state! 

#### Traces - a way of checking a system works! 
- A trace: A sequence of observations
- An obervation: A state, alongside the inputs and outputs at that given state.
- Think of like a trace table.
OMG LOOK ITS A TRACE TABLE!! 
![[Pasted image 20251217120258.png]]
^ note the T instead of 1.

