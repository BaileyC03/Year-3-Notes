#### Clustering VS Classification
- Clustering - Unsupervised learning
	- Class labels of the data are unknown
	- Given data, the task is to establish the existence of classes or clusters

- Classification - Supervised learning
	- Supervision: The data is labelled with pre-defined classes
	- The input data consists of multiple records, each of which has multiple attributes or features
	- Given the training data, the task is to:
		- Develop an accurate description for each class using the features
		- Predict categorical class labels for unseen data

#### Classification continued:
- Training data (Xi, Yi),
	- Xi is typically a feature vector
	- Yi is typically the class label for it
- The task of training is to find a good mapping function f
	- The derived function is then evaluated on unseen (test) data.


#### Support Vector Machines:
- Another method to find the "optimal" linear boundary (or hyperplane) to divide date.
	- This is a binary classification
	- It is looking to maximise the possible margin while minimising classification errors
![[Pasted image 20251222161901.png]]

#### Logistic Regression vs SVMs: 
- Logistic Regression
	- Models the probability of belonging to a class using a sigmoid function
	- It's probabalistic
	- The output is a probability between 0 and 1
	- The coefficients directly indicate feature influence
	- Cross-entropy loss
	-  L2 regularisation controls overfitting

- Static Vector Machines
	- Find the maximum-margin separating hyperplane between classes
	- It's geometric
	- The class label +1 or -1 distance from the boundary
	- It's harder to interpret, the support vector determines the boundary
	- Hinge loss, maximises margin minimises classification errors

#### Cost Function: [EXAMINED PERHAPS]
![[Pasted image 20251222162343.png]]
We are using hinge loss, let's look into it:
![[Pasted image 20251222162423.png]]
If y - 1, we want w^tx >= 1
if y = 0, we want w^tx <= -1
![[Pasted image 20251222162536.png]]
^ The area under the "hinge" is how "shit" it is. 
The left one indicates the data point is either too close to the decision boundary or missclassified
The right one also signifies this
THIS ENFORCES A LARGER MARGIN!
- As being 0 (on the boundary) has loss assigned to it 

#### SVM: Expanded info
The decision boundary is chosen to be the one that has the largest distance to the nearest training data points of any class, as these closest points are called the support vectors. 

These margins establish the maximum distance between the nearest data points of both classes and the decision boundary, which enhances the models ability to generalise.

The width of the margin is inversely proportional to the norm of the weight vector w, expressed as 2/||w||.  AKA a larger margin is achieved by minimising the norm of w

#### Dual formulation of SVM:
- Use the lagrange multiplier and define the lagrange function
- Find the partial derivatives for L(w, b, a) with respect to w and b
- Substitute them back into the original SVM optimisation paradigm
- Why?
	- The dual form lets us use the kernel trick! (explained later)

#### KKT Conditions:
- The optimality conditions for a constrained local optimum are called the KKT conditions (Karush, Kuhn, Tucker) and they play an important role in constrained optimisation theory. 
	- As in you want to minimise f(x), subject to g(x) <= 0 
		- f(x) is the function
		- g(x) is the constraint of the function (aka the region solutions are allowed)
- They are, as follows:
![[Pasted image 20251223121701.png]]
and their meanings, in order:
- The sum of gradients is 0
- Lambda, as the constraint, must be non negative
- Either lambda = 0, or g = 0 (g being the constraint)
- the constrain itself


#### But what if the data is not linearly separable?
- KERNEL FUNCTION GAMING!!!
- The "Kernel trick" is when an SVM converts data (which cannot be linearly separable) into a higher dimensional feature space in which it may be linearly separated.
- It lets you make a hyperplane that separates the data with a maximum margin even if its not separable in normal dimensions
- In the real world, this can be crazy expensive computationally to transform using many polynomial combinations
- To get around this, the kernel "trick" only represents data through a set of pairwise comparisons between the original data instead of explicitly applying the transformations.

#### Kernel: A Definition:
- A function which takes its input vectors from the original space and returns the dot product of the vectors in the feature space.

#### Frequently used kernal functions
- Polynomials of degree d
- Radial basis (Gaussian kernel)
- Neural Network (Hyperbolic tangents)


#### Soft Margin:
- Some samples probably wont satisfy the constraints
- A soft margin has tolerance for the samples which dont satisfy the constraints
- Soft margins allow misclassifications to happen, but this means we will need another constraint
	- This is so we can add a "cost" to missclasifications.
- This parameter is considered the "C" value, it is how you can set the trade-off between  maximising the margin and minimising missclassification loss.
	- Small C -> Maximise the margin
	- Large C -> Minimise missclassification

#### When to use a hard margin?
- When the data is known to be linearly separable
- High precision necessary
- Data is from noise

#### When to use a soft margin?
- Some overlap between classes
- Noisy data
- Needed to be ore flexible and robust to outliers