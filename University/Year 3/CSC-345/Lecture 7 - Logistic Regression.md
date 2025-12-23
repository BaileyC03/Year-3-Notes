#### What is a classification problem?
- The problem of assigning observed samples into a set of labels based on a rule
	- Supervised strategy is when you have known classes or labels available
	- Unsupervised is when you do not have known classes of labels available
- Steps of a classification problem:
	- Split data into a training, validation and test set
	- Use the training data to build a model with the set of parameters and validate the model with validation set
	- Repeat the above step changing parameters until the performance is satisfactory
	- If the training and validation results are ok, then you can use the final trained model to test and report results! 

#### Logistic Regression:
- This is for the type of problem where variable Y follows a binomial distribution
	- Has only 2 outcomes, 1 or 0 essentially.
- Finding the best fitting model to describe the relationship between a binary Y (response) and X (independent variables, predictors etc).
- It's used for anything where the outcome can be one of 2 answers, true/false, success/failure, healthy/cancerous etc. 

- The dependent variable must be between 0 and 1
	- ![[Pasted image 20251222142050.png]]
	- ^ w is the weight assigned i beleve
	- ^ h is the "hypothesis" or dependent variable.

- We also will need our logistic (sigmoid) function
	![[Pasted image 20251222142506.png]]
	^ this looks like an S btw
	![[Pasted image 20251222142528.png]]
	^ imagine all the X axis is actually -0.6 etc... as its x10^-1
- Now combine this function with linear regression
	- Linear regression is Hw(X) = w^T X
	- So we get:
![[Pasted image 20251222142637.png]]

#### Why do we combine it?
- This makes the model learn which features matter and by how much
- The linear function projects all our input features into a single scalar value based on the learned weights.
- We can then apply that sigmoid to the scalar!

#### Probability Interpolation:
Hw(x) can be interpreted as the probability that y =1 given an input x
by the function as so:
![[Pasted image 20251222150647.png]]
this means hypothesis(given weights w, transposed. Also, x) is equal to
the probability (that y = 1 | given our x and given our weights)

#### Linear regression on nonlinear data!
- For nonlinear data, we can sometimes transform the data into a linear one which allows us to turn it into an problem we can get linear with
- ![[Pasted image 20251222150855.png]]


#### Decision boundary
- In a 1-D feature, it is simply a threshold value (i.e. 5, for example)
- In a 2-D feature, it will be a line (can be a circle or any shape)
- In a 3-D feature it will be a plane (can be bent in any way)
- Basically for every n-dimensions, he decision boundary will be (n-1)-dimensions.

#### Linear Decision Boundary
- Takes the two-dimensional feature space as an example:
	- The decision boundary will be a straight line
	- w^T x = 0
	- Positive samples (>0) cant be much higher than 0
	- Negative samples (<0) cant be much lower than 0
- Wrap the decision boundary (line) equation with the log function
	- hw(x) = [g(w^tx) <- between 0 and 1]
	- The output is now bounded!
	- Predict y = 1 if when W^x > 0, g(w^Tx) >= 0.5
	- Predict y = 0 if when W^x > 0, g(w^Tx) < 0.5
		- w^T may be something like (-2, 2, 1)

#### What makes a good decision boundary?
- When y = 1 for a given decision boundary:
	- All of the positive samples, when projected to the sigmoid function g, should be as close to 1 as possible.
	- i.e. the mean of all values assigned to y = 1 should be as close to 1 as possible!
	- The mean *must* be bounded between 0 and 1
- function G is non-linear however so it an be hard to find the optimal solution
	- thus, we apply negative log transform.

#### Cost Function:
- To find the optimal decision boundary, we want to minimise:
![[Pasted image 20251222154431.png]]
- m is the number of positive samples (y = 1)
![[Pasted image 20251222154444.png]]
- n is the number of negative samples (y = 0)
We can combine these samples together however!
- N is the total samples number!![[Pasted image 20251222154719.png]]
^ This is our binary cross-entropy cost function.
We can also regularise it!
![[Pasted image 20251222154817.png]]
which can be factorised to:
![[Pasted image 20251222155053.png]]
This prevents overfitting and can control the complexity of the model.
Remember:
- Too complex a model = overfitting

#### GRADIENT DESCENT IS SO BACK:
Just like linear regression, we find the optimal parameters to minimise E(w) using gradient descent!
![[Pasted image 20251222155329.png]]
where alpha is the learning rate (hyperparameter)
- In order to make a prediction for a new datum (singular of data), X(n+1):
![[Pasted image 20251222155619.png]]
where the result must be interpreted as a probability of y  being 1
	aka <0.5, its y=0
		>0.5, its y=1
		
#### Multi Class Classification:
- Binary Classification (X or Y)
- Multi-class Classification (X or Y or P or Q or Z or ...)
	- Can be done using a "one vs all" strategy
	- For each class, approach it with a binary approach to check
		- "Is is our desired class or not?"
		- if its our desired class, assign it to that class
		- If it's not, try again with another class and ask the same question with a binary technique