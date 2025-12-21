- Input data tends to have a fuck ton of dimensions
- A few of the features are kind of useless and dont help us classify shit.
- A lot of algorithms have their efficiency depending on the number of dimensions we're working with. 
- High dimensional data can also result in:
	- Overfitting
	- Expensive to store
	- Indexing and retrieving data is a bitch
	- Hard to visualise

#### Dimensionality Reduction goals:
- Reduce the dimensionality of the data while maintaining the meaningfulness
- Find a low-dimension but useful representation of the data
- Discover the intrinsic dimensionality of the data
	- Some high-D data is actually low-D as most dimensions are irrelevant. 

#### Principle Component Analysis:
- Linear method to transform data to a lower dimensional space
- Goes from large number of related variables to smaller number of principle components which are uncorrelated
	- ordered so the first few contains most of the variation in the original variables.

#### General terms:
Mean
- Average of all data values
Median
- Value in the middle when the data items are stored in ascending / Descending order
- Often preferred for location if the data has extreme outliers
Variance
- Measure of variability that uses all data (Average of squared differences between values and the mean)
- Also SD squared!
![[Pasted image 20251220130532.png]]

Standard Deviation
- Positive squared root of the variance
![[Pasted image 20251220130541.png]]

#### Covariance: 
So as we know, variance is defined as such:
![[Pasted image 20251220130727.png]]

Thus, the covariance between 2 variables x1 and x2 is defined as:
![[Pasted image 20251220130804.png]]
^ Where E(.) denotes the expected value, or the mean.

The variance is actually a form of covariance!
Cov(X,X) = E[(X - E(X))(X - E(X))]

#### Zero-centred values:
- Subtract the mean (=E[X]) from the observed values
- For zero-centred variables, the covariance simplifies to:
![[Pasted image 20251220131009.png]]
and the variance simplifies to:
![[Pasted image 20251220131023.png]]
![[Pasted image 20251220131453.png]]

#### Covariance: A worked example!
- Obtaining the averages: In this case the mean
- ![[Pasted image 20251220131543.png]]
-  ^ Averages are our expected value, i.e. H with the line on top. HBar.
- So now we have our 2D Data covariance: 
- ![[Pasted image 20251220132309.png]]
-  So now you wanna take the mean of the final column,  which is 104.54 and that is the covariance of H and M! 
- Cov(H,M) = 104.54

#### Covariance for 3D Data!! 
![[Pasted image 20251220132631.png]]
^ Note it will be symmetrical along the diagonal as cov(x,y) is the same as cov(y,x)
- Along the main diagonal, the matrix also contains the variance values
	- Remember, cov(n,n) = variance of n for all n respectively.
The general formula for this is:
![[Pasted image 20251220133912.png]]
We used 1/n-1 somethin somethin degrees of freedom.
Degrees of freedom:
- The number of independent observations in a set of data
- From a single sample of size n, number of independent variables is n-1.

#### Why do we need degrees of freedom?
Consider the following dataset:
- 75, 79, 56, 81, 66, 58, 77, 61, 71, 76
- The mean is 70
- To calculate the standard deviation
	- 75 - 70 = 5
	- 79 - 70 = 9
	- 56 - 70 = -14
	- 81 - 70 = 11
	- 66 - 70 = -4
	- 58 - 70 = -12
	- 77 - 70 = 7
	- 61 - 70 = -9
	- 71 - 70 = 1
	From this, we know what he last deviation *must be*, as they must all sum to 0.  D10 (deviation 10) is completely determined by the other 9.
- When we use the sample mean (x bar) instead of the true mean to compute variance, the result is slightly smaller on average.
- Dividing by n-1 corrects this bias. Known as Bessel's correction.
		- N = number of samples.

#### Creation of a covariance matrix from matrices:
- Assume we have a matrix: ( 3 Dimensions, 2 samples)
- ![[Pasted image 20251220134451.png]]
- First, compute the averages in each diretion
	- [2, 1.5, 2]
- Then, for each column, subtract the averages
	- ![[Pasted image 20251220134555.png]]
- Finally, compute the covariance matrix
![[Pasted image 20251220134647.png]]

- So we have our X', we also want X'^T
	- Tranpose it so swap the x and y.
- Then, multiply X' and X'^T
- Then do the 1/n-1 to the product.

#### What does the Covariance matrix show? 
[A, B]
[C, D] <- Assume this is the covariance matrix, 2x2.
A (cov x,x)-> How wide the spread is
B and C (cov x,y) -> How "positive" the correlation is (negative = negative correlation)
D (cov y,y ) -> How tall the spread is

#### Eigenvectors and Eigenvalues
- The covariance matrix describes how data spreads and how features relate to eachother.
- An eigenvector is the direction in which the data stretches or compresses.
- The eigenvalue tells us how much the data stretches in that direction

Thus:
- The eigenvector with the largest eigenvalue points in the direction of the most data spread

If the covariance matrix has a 0 for B and C (i.e. cov(x,y) = 0) the variances are equal to the eigenvalues!

If the covariance matrix is not diagonal (So the covariances are not zero), it means the data features are correlated.
	- Eigenvectors still show the variance where the data spreads out the most.
	- Eigenvalues still show tell how much the data spreads along the related Eigenvector.
	- Because the data is tilted, the X and Y axis variance no longer describe the spread.

#### Principle Component Analysis!
- Decorrelation method
	- Linearly transforms the daya so that the covariance values are all 0
	- Retains the components with the largest variances
	- Gets rid of components with small variance to reduce dimension.
- In a super informal sense:
	- Get all your data on the eigenvector with the largest eigenvalue
	- Rotate the data until the eigenvector is on one of the axis
	- Squish that bih onto that eigenvector
- Eigenvectoes correspond to principle components! 

#### The major steps of PCA:
- List the eigenvalues of descending order
- Set a threshold and remove the principle components (eigenvectors) with small variances (eigenvalues)
- The data is then projected back with reduced dimensionality

#### How do you actually compute PCA? 
- Consider the data matrix X(n x p) and its square shape covariance matrix Σ(p x p) the roots of the following equation give the eigenvalues (lambda) of Σ:
	- det (Σ - (lambda)I) = 0 where:
		- det means to find the determinant
		- lambda is the scaler and is thus the Eigenvalue of Σ
		- I is the identity matrix -> A matrix with 0 except 1s on the diagonal of size pxp
- For each of the eigenvalues, there is a corresponding eigenvector which can be found by solving
	- Σv = (Lambda)v

- Or, it can be shown in the matrix form:
	- If V = [v1, v2, ..., vp] is the PxP matrix of the eigenvectors, we have the matrix form equation:
		- ΣV = VA
			- where A(pxp) = the diagonal matrix of the eigenvalues.

#### EVD - Eigenvalue Decomposition:
- ΣV = VA  -> (V^T)ΣV = A and Σ = VA(V^T)
- -V is normalised and has unit magnitude
-  They are also orthoganal,  so:
	- (V^T)V = V(V^T) = I.
- Therefore,  (V^T)ΣV = A and Σ = V(V^T)
- This is the eigen decomposition of the matrix Σ which is used to compute V.

#### Example:
![[Pasted image 20251220142936.png]]
^ Ask for a workthrough on this. 

#### Data Projection
- the matrix of eigenvectors can be used for a linear transformation to transform samples from the original coordinate system (x1, x2, .... xp) to a new system defined by V:
	- PC = XV
	- PC = PC1, PC2, ... PCp
- The columns pf PC = XV are called the principle components of X.
	- They are uncorrelated (covariance is 0)
	- and are constructed as linear combinations or mixtures of initial vars.
-  The covariance matrix of the data in the new coordinate system is A, which has zeroes in all the off-diagonal elements.
- Then, each (lambda)i explains the variance of data along each orthogonal direction Vi
	- The directions are sorted based on their corresponding variance.

#### Dimension Reduction:
- Most of the information within the initial variables are squeezed and compressed onto the first few Principle Components.
- Then, out of the P initial variables (P = the feature number before PCA), the first few PCs are retained by PCA including the maximum possible information
- then, the greatest *d* eigen values (lambda1, lambda2 ..., lamdad) that explain most variation within the data are used, and their corresponding columns V = [v1, v2, .... vd] are used.
- ![[Pasted image 20251220144832.png]]
- Instead of P number of variables, only d < P are available.
- t is defined based on the maximum desired variations
- ![[Pasted image 20251220144805.png]]


#### The general steps for PCA: 
- Compute the PCs for the data set:
	- Centre the matrix of samples X to make Xc, such that the mean for all samples' coordinates are 0,0.
		- You do this by taking the "blob" of samples and moving it, as if you had a blender move tool in the graph. The position of the points relative to eachother remains the same.
	- Transpose the Xc to Xc^T
	- Create the covariance matrix from Xc^t, remembering mult by Bessel's Correction (1/n-1)
	-  Compute the eigen values det(Σ - (lambda)I) = 0
		- Aka subtract the lambda identity matrix from Σ, then get the determinant which means to multiply the diagonals in an "X" shape, then just find the roots of the quadratic! 
	- Compute the eigen vectors V = [v1, v2] = [v11, v12, v21, v22] <- pretend this 2x2
		- https://youtu.be/qa9fI6qvUQY
	- Find the main component by comparing the eigenvalues.
		- Larger the eigenvalue, the more expressive the component it
		- Then normalise the eigenvector with the larger eigenvalue to unit length
	- Then, normalise it to be of length 1. 
		- You do this by taking the length of the eigenvector (think pythagoras for x and y),
		- then dividing it by the length as x/x = 1. Do this for the top and the bottom of the vector. So, for example vector of length [1,1] would be [1/sqrt2, 1/sqrt2]
	- Finally, compute the final dimension reduced data set
	- Multiply the centralised dataset by the normalised eigenvector.

#### SVD - Singular Value Decomposition: [I dont think in exam?]
- Does not require a covariance matrix and works directly on the data matrix! 
	- Works on non-square matrices
- Eigen decomposition of Σ is connected to the singular value decomposition (SVD) of the data matrix X[n*p]
- X = USV^tT
	- where:
		- X -> The Original data matrix
		- U[n x p] -> Orthogonal U^T U = I, the columns are called the left singular vectors
		- V [p x p] -> Orthogonal Eigenvector matrix and vi are the right singular vectors
		- S[p x p] is a diagonal matrix with diagonal elements.
- 





