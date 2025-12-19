#### Hard VS Soft Clustering
- K means Clustering -> Hard Clustering
	- Non-overlapping clusters
	- One point can only be in one cluster at a time
	- Clusters are perfectly circular
- GMM -> Soft Clustering
	- Overlapping clusters
	- A point is in all clusters at the same time, with a differing probability of each
	- Non-circular clusters

#### Conditional Probability:
- The probability of an event occuring given a previous event has happened.
- Calculated by multiplying the probability of the first event by the updated probability of the second event
	- P(A|B) = (P A and B) / P(B)
- You know P(A and B) = P(B and A) and that P(A|B) P(B) = P(B|A) P(A)

#### Conditional Probability - Bayes Theorem *
P(A|B) = (P(B|A) * P(A)) / P(B)
where: 
- P(A|B) = Probability of A occuring given B has already occured
- P(B|A) = Probability of B occuring given A has already occured
- P(A) = Probability of A occuring before evidence it has/hasnt
- P(B) = Probability of B occuring before evidence it has/hasnt
^ P(B) is calculated as the sum of all probabilities of B ocuring given each event Ai, multiplied by the probability of Ai occuring accross all possible Ai events. 

#### Confusion Matrixes: 
- X axis - Prediction
- Y axis - Actual labels / truth
-  The higher the percentage of the diagonals, the better! The diagonals are correct predictions!
![[Pasted image 20251218122152.png]]

#### Distribution:
- Uniform distribution - Where all outcomes are equally likely
- Normal distribution - "bell curve" - where values are frequently occuring around the mean and are less likely to occur as data gets further from the mean.
	- 2 primary parameters:
		- Mean - Determines the centroids
		- Standard deviation - 68% of values fall within 1 standard deviation of the mean. 95% from 2. 

#### Probability Density Function:
- Shows where a continuous random variable is more or less likely to take certain values
- Probability is DIFFERENT to probability dentisy
	- Sum: ΣP(a) = 1 [for discrete probabilities]
	- Integral ∫+-inf PDF(A)d(A) = 1 [for continuous densities]
	- Individual probabilities ∀x ∈ P(A) <= 1
	- Individual density values ∀x ∈ PDF(A) can be greater than 1
	- y axis is the PDF value and shows how likely values around x are to occur
	- the % under the curve is the probability of a sample falling into the area
![[Pasted image 20251218122910.png]]

![[Pasted image 20251218122923.png]] 
^ OMG ITS THE NORMAL PROBABILITY DENSITY FUNCTION! YOU MUST KNOW THIS!

#### Arbitrary distribution
- No known PDF to represent arbitrary distributions
- Generally, data may fall into unknown distributions
- Approximately clusters with unknown distributions can be modelled by clusters with mixture of known distributions

#### Gaussian Distribution:
- Also known as a normal distribution (1 Dimension)
![[Pasted image 20251218122923.png]]
- μ is the mean
- σ is the standard deviation
- A single gaussian function is usually not sufficient to model things.
- Real world data is often multimodal 
	- Characterised by many maxima (many curves)


#### Understanding covariance matrices for 2D GMMs: 
[1 x] -> If x is 0, the dist is a circle. As it goes up, it thins and points 45 clockwise.
[x 1] ->  Goes down, thins and 45 anticlockwise. Greater the number, closer to a line it is

![[Pasted image 20251218125908.png]]
OMG ITS A 2D COVIARIANCE MATRIX FOR A 2D GMM! 
- σ11 is the variance of x1, it controls the spread of axis x1
- σ22 is the variance of x2, it controls the axis of x2 
- σ12 and σ21 are the covariance between x1 and x2. 
	- They control the tilt and elongation of the ellipse

#### Observations of the elements in a 2D Gaussion Covariance Matrix: 
- σ12 = σ21 every single time
- If σ12 and σ21 are POSITIVE, there is a POSITIVE correlation between x1 and x2.
- if σ12 and σ21 are NEGATIVE, there is a NEGATIVE correlation between x1 and x2.
- if σ12 and σ21 are 0, there is NO consistent relationship between x1 and x2

#### Gaussian Mixture Models:
- We can use a mixture of gaussian functions to learn the distribution of data
- The distribution is modelled by a set of parameters: 
	- k, the number of gaussian functions (curves)
	- μ, the mean for each gaussian function 
	- σ, the standard deviation for each gaussian function for 1d, or the covariance matrix for each gaussian more generally.
	- P, the mixing coefficients, the weight of each gaussian function
- These bitches are good for modelling multimodal distribution.
- GMM is described as a weighted sum of Gaussian functions
![[Pasted image 20251218131248.png]]
where: 
- P(j) is the mixing coefficient, known as the prior probability
- The sum of all P(j)s add to 1
- j indicates gaussian function number j in the GMM.
- In a >1D scenario, each gaussian function is instead given as: 
![[Pasted image 20251218131408.png]]
where:
- d is the number of dimensions
- Σ is a d*d covariance matrix; for all 1D, Σ = σ^2
- thus, 
![[Pasted image 20251218122923.png]]


#### Transposition of a Matrix:
- In linear algebra, the transposition of a matrix is an operator which flips a matrix in a way that it switches the row and column indices.
	- 1,2 becomes 2,1
	- x,y becomes y,x etc...
- For matrix A, it can be noted as A^T

#### Gaussian Mixture Models: Continued
- Each component in the GM has its own gaussian distribution assigned finally.
- Every cluster has its own size (mean, SD) or correlation (covariance matrix) with others. 
- You must comput the probability that a each data sample belongs to each cluster by computing posterior probability p(j | x)
- each cluster is approximately modelled by updating the gaussian distributions, its iterative

#### The Major Steps of GMM, Step 1: Initialisation:
- Learning the GMM Parameters.
	- mean, (standard deviation or covariance matrix), mixing coefficient.
	- K is given
- Start from an initial guess of the parameters using something like K-means
	- Standard deviation or covariance matrix can be computed from the clustered data
	- P is computed by counting the number of data belonging to each component (aka cluster) 

#### The Major Steps of GMM, Step 2: Posterior Probability:
- Based on initial expectations, we can now compute the posterior probability
	- Given by bayes theorem
	- P(J|X) = (p(X|J) * p(J)) / p(X)
		- AKA he probability the given data x belongs to component j
	- Remember: p(X) = [sigma j  is each component] p(X | J)P(J) <- upcase P is the mixing coeficient
	- Also: (where sigma is the covariance matrix and lowercase sigma is the SD)
	![[Pasted image 20251218133738.png]]
#### The Major Steps of GMM, step 3: Updating parameters:
- Now we can update our parameters where (x^n is the index of the data)
![[Pasted image 20251218133919.png]]
The mixing coefficient is simply the normalised summation of posterior probability
![[Pasted image 20251218133928.png]]
The posterior probability weighted mean
![[Pasted image 20251218134004.png]]
The posterior probability weighted covariance matrix

#### GMM: Overall
- Iterate steps 2 and 3 until stabilisation, maximising the log posterior probability
- In summary:
	- Estimate mean, SD and mixing coefficient (k sets of them, k being the number of curves)
	- K-means clustering to get initial values
	- Then repeat the following until convergence:
		- Computer posterior probability for each data point
		- Update parameters accordingly

#### K-means vs GMM:
- K means:
	- Hard clustering, each data point belongs to exactly one cluster
	- Each point is assigned full (100%) to its nearest cluster
- GMM:
	- Soft clutergin, Each data point belongs to every cluster with a probability 
	- The total probabilities should add to 100%, or 1 if not a percentage.
- Both:
	- Both produce local solutions
	- The iterative process greatly depends on the quality of the initialisation
	- They are both sensitive to outliers
	- They both require pre-defined K values
	- They are both iterative processes