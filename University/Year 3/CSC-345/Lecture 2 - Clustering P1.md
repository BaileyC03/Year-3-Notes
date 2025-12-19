#### Clustering:
- Given a cloud of data points, understand its structure.
- A process to find similarity groups (clusters) in data.
	- Group instances that are similar to eachother in one cluster
	- Instances that are different / far are in different clusters
	- Clusters are unlabelled an no prior knowledge exists on them before clustering
		- Thus, this is unsupervised learning.

#### Approaches to Clustering:
- K-means
- Fuzzy C-means
- Gaussian Mixture Modelling (GMM)

#### Clustering and dimensions
- Clustering in low dimensions with small amounts of data is straightforward
- It is however common that clustering needs to be performed in very high dimensionality space
- Data samples required grows exponentially with the increase of dimensionality
- In high dimensional spaces, most data points are far from eachother and the difference in distances decreases. 

#### K-means clustering
- A partitional clustering algorithm
- Number of clusters is pre-set (K)
- Each cluster is represented by the centre of that cluster
- Each data point is assigned to the nearest centre (i.e. centroid)
- Iterative process, starts with a completely random initialisation of centroids

#### Minimising error of clustering?
- Minimise SSE (sum of squared error) such that:
	- For each centroid, take the squared distance of every data point from the nearest  centroid
	- Look to minimise this based on data partitioning (i.e. slap the centroid in the mean of all of its clustered nodes)
		- Literally average the X and Y of all nodes related to it.
	- Continue these steps until some stopping condition met (usually a lack of difference of SSE)
	- 