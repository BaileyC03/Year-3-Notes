#### Limitations of PCA:
- Unsupervised analysis (No class labels)
- If we have class labels:
	- PCA may not be optimal for classification or dimensionality reduction
	- In PCA, global data variation determines the projection orientation
	- Basically, PCA may group different classes together if the most expressive tells it to, in the case of long clusters or something/
- What makes a good projection if we know the labels?
	- Reduced dimensionality
	- Preserves the clusters and their separation


#### Useful class information:
- Between class distance
	- How far the centroids of both classes are

- Within-class distance
	- The sum of distances from all points to the centroid of the class it is assigned to

#### LDA - Linear Discriminant Analysis:
- LDA finds the most discriminant projection by:
	- Maximising between class distance
	- Minimising within class distance

- Assume we have a set of 2D samples 
	- {X1, X2, ... Xn}
			- So each of these samples Xi = (Xi1, Xi2)
		- N1 of these samples belong to class w1 and N2 of belong to class w2
	- We seek to obtain scalar (magnitude) y by projecting the samples X onto a line 
		- w defines the projection eigenvector
		- y = W^t X
		- Of all possible lines, we want ot pick the one that maximises the separability of the scalars.
![[Pasted image 20251220160654.png]]
^ Notice how it always goes through 0,0. 
- In order to find a good projection vector (W), we need to defined a measure of separation!
	- The mean value of each class in x and y feature space
![[Pasted image 20251220160751.png]] -> The between-class distance
![[Pasted image 20251220160810.png]] -> The within-class distance. 

#### Linear Discriminant Analysis, continued: 
- the distance between the 2 projected mean values offer a measure of how separated the 2 classes are after projection.
-![[Pasted image 20251220160856.png]]
- However, this is not the full picture as  there is more to separability than just mean distance. 
- The solution?
	- Maximise the distance between the means
	- ALSO minimise the measure of the within-class scatter
		- Scatter - THE SUM OF SQUARED DISTANCES FROM THE MEAN


#### Fisher's Linear Discriminant Method:
- The linear function W^T X that maximises the critetion function J: [EXAMINED]
![[Pasted image 20251220161723.png]]
^ J is what we are looking to maximise
- S1^2 and S2^2 are scalars
- We are looking for a projection where the samples from the same class are projected very close to eachother and, at the same time, the projected means are as far from eachother as possible. 
	- The computational challenge is finding W -> W is the projection vector! the line! 

#### Fisher's Criterion (Rayleigh Quotient):
- We must optimise the objective function in order to find w
- First, you want to find the scatters for each class
![[Pasted image 20251220162255.png]]
- The definitions of Ui and Si^2 are both defined based on the vector w.
-  The within class scatter (si^2) can be formulated based on the Eigen decomposition formula
![[Pasted image 20251222112925.png]]
^ Remember, sigma here is the covariance matrix!
Si^2 is a scalar based on the eigen decomposition of each class' covariance Σi 
Consider, 
![[Pasted image 20251222115215.png]]
and 
![[Pasted image 20251222120941.png]]

Thus, 
![[Pasted image 20251222121046.png]]
^ Note it;s literally just factorisation on the top and the bottom. 
- Also, w^T Σ1 ​w = the spread! It's literally just row \* matrix \* column
- What is the || ||? The length!
	- The 2 over 2 at the end is the euclidean norm of whatever is inside the bars, then square it!

#### Generalised Rayleigh Quotient
- We intend to find this *W* based on the formula:
![[Pasted image 20251222121931.png]]
^ Note, the denominator must be non-zero but as small as possible!
[The top one is between class scatter, the bottom is within class scatter]
We also want to maximise the numerator
Thus, in reality we want to maximise:
![[Pasted image 20251222122231.png]]
^ The first part here is the numerator                                             ^ This is the denominator where K is 
													a defined constant which we use as a constraint in the optimisation problem! Essentially if we have a solution, the scale of the denominator will not matter.

#### We solve this using the Lagrange method!
![[Pasted image 20251222122354.png]]
^ the alpha α is the lagrangian multiplier, a scalar introduced to enforce a contstraint during 
optimisation.
From here, you can do gradient descent! 

#### How to find the projection direction "W"
- AKA how do you find the direction in the feature space in which the data should be projected to max class separation compared to within class spread. 
![[Pasted image 20251222123828.png]]
^ Sw is within class spread, the ^-1 makes it 1/Sw
AKA this whole thing could be considered (Sbw)/Sw = aw

#### Method 1: Generalised Eigen Decomposition
Det(Sw^-1Sb - (lambda)I) = 0
![[Pasted image 20251222124158.png]]
(Lambda is the same as alpha, the symbol has just been changed for shits and giggles)
^ Lambda tells you how much class separability exists! So we can consider it as J(w)
![[Pasted image 20251220161723.png]] 
^ THIS J(w)!
So now, we can use the EVD equation from PCA to find W!
![[Pasted image 20251222124342.png]]

#### Method 2: Do that bih directly with a guesstimate
![[Pasted image 20251222134624.png]]
meaning w is approximately this, where:
	Sw is the within-class scatter matrix
		^-1 means you need to inverse the whole matrix
	then, multiply it all by mean1 - mean2 but transposed to 1x2 matrices.
	Heres an example!!
![[Pasted image 20251222135406.png]]

#### Reminder: The cost function of LDA? 
![[Pasted image 20251222132131.png]]

#### WORKED EXAMPLE OF LDA:
- Find the means of both classes (mean the x values and mean the y values, simple. Then you have your X,Y coord of the mean!)
![[Pasted image 20251222135458.png]]
- Then, create a scatter (covariance) matrix for each class:
	- Treat each x,y like a 1x2 matrix, where you subtract the mean from both coords and square it.
	- Sum this up for all of them!
	- You should be left over the covariance matrix for the total class:
	- ![[Pasted image 20251222135658.png]]
	- Simply do the same thing for the other class(es) also
	- ![[Pasted image 20251222140027.png]]

- From here, you want to find the within-class scatter Matrix Sw:
	- Sw = S1 + S2
	- ![[Pasted image 20251222140129.png]]

- You will also want to find the between-class scatter matrix Sb
	- Sb = (u1 - u2)\*(u1 - u2)^T
	- ![[Pasted image 20251222140210.png]]

- Finally, you can solve the optimal projection weight directly!
	- W = S\^-1W(u1 - u2)
![[Pasted image 20251222140351.png]]

#### But how do you calculate a matrix to the power of -1? 
IM GLAD YOU ASKED!
![[Pasted image 20251222140716.png]]
Basically you just do this shenanigans:
![[Pasted image 20251222140738.png]]

#### We will simply not be using EVD for this in a worked example because it hurts.

#### WHAT IF YOU HAVE MULTIPLE CLASSES EH!?
- Process is the same:
	- Create an axis that maximises the distance between the means for the 2 categories while minimising the scatter
- but:
	- We seek C-1 projections (1 less projection than we have original classes)
	- Also, you measure the distances from means to a centroid in the middle

#### LDA vs PCA? 
- LDA is supervised
	- Has different centroids
	- Can be supported by bayes theorem 
- PCA is unsupervised
	- May have overlapping centroids
-