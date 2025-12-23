#### ANN - Artificial Neural Network Structure
- Simplified model of how human neural systems work
- Simulate natural information processing tasks akin to the human brain
- The output of an ANN is a function of its inputs:
	- Y = F(X)
- Complex model, cant be easily approximated

#### ANN Description:
- Used to learn the complex model based on some training data
- (It looks to learn the right parameters)
	- Parameters of the model are the weights connecting each node.
	- They are learnt using existing supervised samples in the training process
	- Once the weights (params) are learnt, it can be used to predict or make decisions.

#### Perceptrons!
![[Pasted image 20251223124537.png]]
- w is the weights
- x is the input nodes
- note how the top one is a constant! OMG ITS BIAS! how simply goated?
![[Pasted image 20251223124909.png]]

#### Logistic Units!
- A graphical representation of a logistic function (The red circle)
![[Pasted image 20251223124934.png]]
![[Pasted image 20251223124955.png]]

#### Logistic Function - The activation function of a given layer.
- Also known as the sigmoid function
- The dependent variable needs to fall within the range of 0 and 1
- If wTx < 0, the g(wTx) < 0.5
- If > 0, its between 0.5 and 1

#### Have a look at this bad boy:
![[Pasted image 20251223125330.png]]
^ Note how when we apply the activation function, we get some non-linearity going on 

#### Neural Network Components:
- The Architecture
	- The pattern of the connections between the neurons (Each link will have a weight assigned to it, these are the parameters remember)
- Weights
	- The method of determining the parameters on the connections known as the training algo
- Nonlinear Activation
	- The activation function (think sigmois, relu etc)

Note: we usually dont draw the bias units.
#### Input / Output:
- All nodes past layer 2 takes input as the output of the later before it.
- These outputs are the learned results of the layers.

#### Binary Classification:
- A single output node works. >0.5 is positive, less than is negative

#### Multi-class classification:
- If the output has >=3, you will need multiple output nodes
- You can then take the node with the highest value as the classification
- The trainin data will be prepared as:
	- The (Label, Vector oaurs)
	- Labels are in the format of matrices representing the output nodes output for the right answer.
![[Pasted image 20251223131208.png]]
^ Known as one-hot encoding (where one entry is "hot" or 1, and the others are 0)

#### What is the training of an ANN?
- Learning the weights from the existing training set to generalise the model for future, unseen data.
- Minimise the error on both the training and data set, while only seeing the training set.

#### 2 Main types of Neural Network Learning:
- Supervised learning
	- Has a teacher telling uou what the output should be for a given input pattern.

- Unsupervised
	- No teacher, learns by itself, no ideal output for the given input patterns

#### Forward Propagation:
- During forward propagation, the output of a  node is a function of its inputs.
- The inputs to a node, which are the product of preceeding nodes are summed up and passed through an activation function before being sent out of the node. 
- The neural network learns using its own (previously learned) features.

#### Backward Propagation
- Backward propagation of errors
- A common method of training neural networks alongside an optimisation method like gradient descent.
- Calculates the gradient of a loss function with respect to all of the weights
- It then feeds this to the optimisation method which uses it to update the weights to try to minimise the loss.
- BUT:
	- Requires a known desired output to calculae the loss function
	- Requires the activation function be differentiable (To get the derivative or gradient)

#### Neural Network Cost Function:
![[Pasted image 20251223132117.png]]
K is the number of output nodes
N is the number of input samples

If you split the equation into 2 parts, before and after the "+":
Basically the first part gets the average sum of logistic regression on the output nodes
The second part is the regularisation term - the sum of the squares of all the weights! 

#### Forward-Backward Propagation
- Backwards Propagation
	- Aims to minimise the cost function by adjusting the weight and biases
	- The level of adjustment is determined by the gradients of the cost function with respect to the parameters (Differential)

- Summary of the algorithm:
	- Set the learning rate as n
	- Set the initial weight values (and bias) W, b -> Can be random values
	- Loop the following until the stopping criteria satisfied:
		- For each of the samples in the training set [FORWARD PASS]
			- Present an input pattern to input units
			- Compute the output signal for the hidden units
			- Compute the output signal for the output units
			- Present the target response to the output units
			- Compute the error for this sample
		- Compute an overall error for all the patterns (Depending on your loss function, cross entropy for example) [Backward Pass]
			- Update weights at the output layer
			- Update the weights at the hidden layer
			- Increment t (t is the epoch number)

	- Each full run forward and back is considered an "epoch"
	- It is better to randomise the order of training patterns presented in each epoch
		- Prevents pairwise correlation being learnt
	- The stopping criteria can be X epochs, or X level of error on the training set.
	- The choice if the initial weight values is important as it decides the starting position for the weight space.

#### Types of Weight Initialisation
- Zero initialisation
	- All weights are set to zero in order to start with
	- This can be a problem as all nodes will behave the same
- Random initialisation
	- Breaks symmetry and every node computes differently

#### Neural Network Architecture:
- Number of hidden layers
	- Determines the depth of a neural network
	- The more hidden layers, the more powerful the NN is
		- More expensive to train
		- More prone to overfitting as it has more hidden nodes
- When do you need more nodes?
	- Low values of both training AND validation data
- Try to have your nodes in layers in the following order:
	- X\*2^n , X\*2^n-1 , X\*2^n-2 , etc... 
	- AKA halving each tme

#### Overfitting:
When the training set is much more accurate than the testing set, you are overfitting!
How to fix this?
- Drop-out (setting some output features to 0 randomly during training)
- Less hidden nodes

#### Batch Gradient Descent:
- Using logistic regression, we want to find parameters to minimise the cost.
	- Using gradient descent
- This is an iterative process!
	- For each iteration, the partial derivative calculation involves enumeration across the entire dataset (all N samples)
	- This type of gradient descent is known as batch descent as it does it all in one batch
	- Can be expensive on large N 

#### Stochastic Gradient Descent
- Instead of summing over all data points, which is expensive you can:
	- Randomise dataset through shuffling
	- Perform gradient descent on a single data sample
		- Sometimes a small subset of data samples instead!

#### Approximate "AND" as a perceptron!
![[Pasted image 20251223202443.png]]
The weights -30, 20, 20 would make this an "AND" operator as
the bias will give you -30 - meaning the x1 and x2 would both 
need to be "on" or "1" in order to, when mutliplied by 20, sum to >30.

The weights -10, 20, 20 would make this an "OR" operator for the
same reason as above but now 1+ inputs can be present for it to sum >10.

![[Pasted image 20251223202628.png]]
For something like this, a "NOT" operator could be done with weights -10, 20

#### XNOR: 
![[Pasted image 20251223202807.png]]
Basically, X1 and X2, or (Not X1) and (Not X2)
You can take the 2 gates, set their output to 2 nodes in a "combining" final layer that does any finishing touches needed. 
- Consider modelling it like a tree like you have before! :o 



