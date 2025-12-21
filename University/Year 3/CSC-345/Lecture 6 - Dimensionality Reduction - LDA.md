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
- The linear function W^T X that maximises the critetion function J:
![[Pasted image 20251220161723.png]]
^ J is what we are looking to maximise
- We are looking for a projection where the samples from the same class are projected very close to eachother and, at the same time, the projected means are as far from eachother as possible. 
	- The computational challenge is finding W -> W is the projection vector! the line! 

#### Fisher's Criterion (Rayleigh Quotient):
- We must optimise the objective function in order to find w
- First, you want to find the scatters for each class
![[Pasted image 20251220162255.png]]
- The definitions of Ui and Si^2 are both defined based on the vector w.
-  The within class scatter (si^2) can be formulated based on the Eigen decomposition equation
- 