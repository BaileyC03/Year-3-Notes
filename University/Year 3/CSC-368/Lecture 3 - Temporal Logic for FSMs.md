#### Temporal Logic:
- Ensure timely transitions between states based on specific time conditions or events
- Synchronise with external time-dependent processes (i.e. a motor doesnt operate infinitely fast thus does take time)

#### Operators:  (Can be put in the guard section of a transition or in the state to assign shit.)
- after (n, sec) -> Evaluates to true after n seconds.
- at (n, sec) -> True at exactly n seconds
- before (n, sec) -> True if fewer than n seconds have passed
- Every (n, sec) -> Triggers every n seconds.
[ Time can be sec / msec / usec for seconds, milliseconds and microsectons]
^ Note, you can use boolean operators with these also! For example after(2, sec) ^ input = 3/ 
- temporalCount(sec) -> Store the number of seconds since the state became active
- elapsed(sec) -> same as above
- Count(c) -> returns the number of times the chart has woken up since the conditional expression C became true and the associated state became active.
- duration(C, sec) -> returns the length of time that has elapsed since the conditional expression C became true and the associated state became active.

#### Ways to use temporal operators: 
![[Pasted image 20251217122116.png]]
^ Assigning y to be the amount of seconds elapsed since the state became active (aka how long you stay in this state)
![[Pasted image 20251217122355.png]]
^ Assigning y to be the number of chart executions since x became greater than 7.
- Once (the amount chart executions in which x > 3) is greater than 7, it may make the transition.
![[Pasted image 20251217122859.png]]^ Store the number of miliseconds in which x has been greater than 3 in the variable y.
- Transition out of the state once x has been greater than 1 for longer than 0.2 seconds.

#### Types of state action:
- Entry Action - Occurs when the state becomes active -> **en**
- During actions - occurs on a time step in which the state is already active and the chart doesnt leave the state -> **du**
- Exit actions - Occur when the chart transitions out of the state -> **ex**

#### States can be actions such as "MoveUp" or "MoveDown", not just "Floor1, Floor2" etc.... - depends on what you wish to do.

