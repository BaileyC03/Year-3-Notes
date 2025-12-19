#### What is a control system?
- Systems that are used to maintain a desired result or value

#### Open Loop Control Systems: 
- Systems used with processes that require the sequencing of events by "on / off" signals.
- Note, these have an absence of explicit feedback.

#### Closed Loop Control Systems
- Closed loop control systems have direct feedback, and thus have error
- Error - the difference between the required value and the actual value
![[Pasted image 20251218105951.png]]
An example of this would be a heating system,  in which the error would be passed into the system as a "actual current temp" in which our new desired temp increase would be "DesiredTemp - CurrentTemp" 
- The subtraction here makes this a **Negative Feedback Loop**

#### System gain (Negative Feedback)
- G(overall) = y / x
- Error = x = Hy
- Then the input = x - Hy (as error is passed into it)
- We can consider the output of G to be G(input)  -> As if function G applied to the input.
- Thus, we can consider output to be  G(x - Hy)

- System gain y = G(x - Hy)
- y = Gx - GHy
- y + GHy = Gx -> Making Gx the subject of the equation
- y(1 + GH) = Gx
- y = GX / (1 + GH)
- y / x = G / (1 + GH) -> divided both sides by x
^ We know G(overall) = y/x
	thus, G(overall) = y/x = G/(1 + GH)

^^ In the event of positive feedback, literally just flip the sign to be "x + Hy" instead of "x - Hy" 


#### Transfer Functions:
- When considering the inputs and outputs of time, the relationships between the input and output is given by a differential equation!
- G(s) = y(s) / x(s) where:
	- G(s) is the system
	- X(s) is the input
	- Y(s) is the output
- We do however know that Y / x = G/(1 + GH),
-  Thus we substitute G for G(s) and H for H(s) and boom! We're cooking!

#### PID Control:
- Proportional - The magnitude at a certain time
	- Reacts to the current error.
	- Larger error = Larger corrective action
- Integral - The area under the curve at a certain time
	- Integrates the error over time
	- Persistant error over time = Larger correction
- Derivative - The gradient of the curve at a certain time (Differentiation)
	- Predicts future error based on rate of how fast the error is changing
	- Looks to dampen the systems response to avoid overshoot
	- Sensitive to noise