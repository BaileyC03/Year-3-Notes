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