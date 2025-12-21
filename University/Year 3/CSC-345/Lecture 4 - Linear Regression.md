#### What is Linear Regression:
- Slapping a line on that bih.
- A supervised learning algorithm
	- The data contains both the data points themselves and their correct answers
	- The task is to train the machine to predict answers for unseen data
 - Regression
	 - (mostly) Continuous output
	 - Can be fit on linear and nonlinear data, but focus is on linear in this
	 - Technique is a foundation for a lot of advanced algorithms as it represents decision boundaries.

#### The goal:
- To estimate Y' given a linear function on data x:
	- Y'n=1 = w0 + w1\*x(n+1)+1,1 + w2 \* x(n) + 1,2
	- This example the input data is 2d ^
	- w0, w1, w2 are the numbers we wish to estimate!

#### Steps:
- Choose the regressor
	- Start with something that looks about right
	- In order to evaluate its quality, we define a "cost function" which will quantify the fitting
		- LMS! (Least mean square!)
			- Basically looks to minimise the SSE (Sum of each points' distance from line, squared)
	- Perform gradient descent from new point vs old point, where the gradient is as close to 0 as you can get, you've cooked! 
- Gradient Descent:
	- To  find the solution to LMS (Least mean squares), we gotta employ GRADIENT DESCENT!!
- Our cost function is:
	- ![[Pasted image 20251218143423.png]]
	- And our parameters are updated as such:
	- W(t+1) = W(t) + ΔT 
				- ^ Finite change at timestep T where:
				- ΔT = A\*gradient
	- Bigger gradient = bigger steps
	- Bigger learning rate (A), bigger steps
		- Too large A, may miss optimal
		- Too small A, may take fucking YEARS
	![[Pasted image 20251218142724.png]]
	![[Pasted image 20251218142733.png]]
- Note on the second formula, the alpha is the "learning rate" which determines how large the steps are! 

#### How do we find the optimal parameters? 
- Set the partial derivatives to zero! (i.e. we are at the lowest point of the curve)

#### All in all:
- Given the linear regression model:
![[Pasted image 20251220113618.png]]
- And  our loss function: (Note you can subtitute y^ with the above equation)
![[Pasted image 20251220113636.png]]
- And our gradient
![[Pasted image 20251220113726.png]]
Different parameters ^ V
![[Pasted image 20251220113742.png]]
and our learning rate a = 0.01
and our data (1,2), (2,4), (3,8), (4,10), (5,15)

-  Initialisation - Set our w0 and b0
	- We begin by setting w0 = 1, b0 = 0

-  Compute the gradient - Calculate the gradient of the cost function
	- You must calculate the loss function first, and then get the gradients based on the loss value.
	![[Pasted image 20251220120841.png]]
	![[Pasted image 20251220120848.png]]
	^ Notice how its literally just substitution btw

- Update the Parameters - Use the gradient to update the parameters!
	- As we now have our gradient for b0 and w0 (above 2 formulae) we can now update our new ones by subtracting the (learning rate * gradient) 
	![[Pasted image 20251220121603.png]]

- Finally - Repeat this until the model converges! 
	- i.e, Additional iterations result in miniscule or 0 change.
	- For the above example, the optimal parameters are:
		- w* = 3.2
		- b* = -1.8

#### How do we go from single variables to multiple?
- Our model becomes something more like this: 
![[Pasted image 20251220122933.png]]
- And our loss function is 
![[Pasted image 20251220123038.png]]

Thus, we can substitue y^ again. 
Our gradient now is done on a w(n) basis, so:
![[Pasted image 20251220123118.png]]

... And I believe you can continue from here as normal 

#### Nonlinear Transformations: 
- We can pull some bullshit like this to become powerful function approximators
- ![[Pasted image 20251220123640.png]]
- ^ Here, predictions are still linear in terms of W0, W1, ...., thus the maths can be the same! 

#### Polynomial Fitting:
![[Pasted image 20251220123718.png]]
Omg this can be done by:
![[Pasted image 20251220123804.png]]
Or if you want to be more general and allow non-polynomial options:
![[Pasted image 20251220124051.png]]
^ The phi |o lookin thing is the basis function and can be polynomial!! (as seen above) 
or gaussian! (as seen below) 
![[Pasted image 20251220124124.png]]

#### Overfitting & Underfitting:
- Overfitting:
	- Small training loss, large testing loss.
- Underfitting:
	- Large training loss, Large testing loss

Think like goldilocks, we want this to be "just right".
 How can we avoid overfitting? 
 - Early stopping
 - Reduce model complexity
 - Increase sample number
 - Regularisation


#### Regularisation explored: Quadratic Regularisation
![[Pasted image 20251220124329.png]]
^ Adding an extra chunk on the end of the cost function where lambda is our regularisation coefficient. We define this ourselves as its a hyperparameter. 
- 0 -> High risk of overfitting
- 10^-4 to 10^-2 -> Slight regularisation, reduces small noise
- 10^-2 to 10^1 -> Common default range
- 10^1 + -> Good chance we underfit here

#### Bias vs Variance: 
- Bias -> Difference between mean of predictions vs mean of truths
- Variance -> How spread out predictions are, regardless of how close to the truth it is

