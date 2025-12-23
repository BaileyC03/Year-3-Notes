
#### Convolution as opposed to fully connected neural networks:
- A fully connected neural network has every node in a given layer connected to every node in the succeeding layer.
- In a convolutional neural network, it is only connected to 3 or so.

#### 1-Dimensional Convolution
- Flip the kernel left ot right
- Step the kernel along the signal one data point at a time
- At each position, calculate the dot product of the two
	- Multiply each pair of aligned values together
	- Add up those products. 
- The resulting sequence of dot products is the convolution of the kernel with the signal
![[Pasted image 20251223203229.png]]
- For the first block on the upper layer, its (1x1 + 0x1 + -1x2)
- note how the next layer is smaller? This can be changed with padding if you wish to. 
- Zero padding adds 0s on the edge so that the resulting layer is the same size as the input layer.
- Stride is the number of "steps" the filter moves in one go. 

#### Convolution in Neural Networks: 
- Convolution replaces the fully connected
	- The coloured edges represent the elements in the kernel
	- Values in the kernel = the weights on the edges
	- Shared kernel means shared weights
	- Connections are local, instead of global to the entire layer.

- Nonlinear transformation: activation
	- Convolution is a linear calculation
	- Linear transformations arent powerful enough to solve a complex problem
	- Akin to a fully connected neural network, a nonlinear transformation through an activation function (like sigmoid [logistic regression]) is needed.
	- Bias units for each filter

#### Da activation function
- ITS IMPORTANT TO NOTBE LINEAR BECAUSE DATA IS KINDA COMPLEX SOMETIMES
![[Pasted image 20251223204653.png]]
^ What a linear function would be doing to some of these images.

- The activation function transforms the linear convolution operation to nonlinear! 
- The more hidden neurons, the more complex the fit is likely to be. 

#### Activation Function Options:
- Sigmoid function
	- Output within 0-1
	- Continuous function, differentiable everywhere!
	- Somewhat expensive to compute
	- Not zero centered (not epic for training optimisation and efficiency)
	- Gradient vanishes quickly when leaving zero which can stop parameter updates.

- tanh function
	- output within -1 - 1
	- Zero centered
	- Has the same vanishing gradient issue

- ReLu function
	- Does not saturate in the positve region
	- Very efficient
	- Converges faster than sigmoid
	- Not zero centered
	- No gradient in the negative so can lead to dead activation units
		- Must be initialised with a small negative bias

- Leaky ReLu
	- Does not saturate
	- Equally as efficient as relu
	- Converges fast
	- No dead activation units!
	- Still not zero centered

#### 2D Convolution:
- The input is going to be an XxY image and you will have some kernels you are going to
	slide on over. Like so:
![[Pasted image 20251223205617.png]]
^ Note that padding exists for this too. 
Stride is how much it moves horizontally.
- So anywhos you do this with your filter
- Then you can do it with another filter, for however many filters. 
	- Youll end up with a 3D feature map of each object.

 THE FILTERS ARE THE NETWORK PARAMETERS WHICH WILL BE LEARNED! :O

#### Zero Padding:
![[Pasted image 20251223210209.png]]
Keeps ya output the same size as ya input.

The number of parameters = (Filter size x Input Channels x Input Channels + (1 for bias)) * Filter number
	RGB has 3 channels for example
CNNs have less parameters than fully connected neural networks!

#### The Whole CNN System:
- Convolution
- Max Pooling
- Convolution
- Max Pooling
(Basically do conv -> pooling as many times as u wanna) 
you will have 2d feature map(s) by this point
- Flatten
(1D vector -> the feature vector taken as input for a FCNN)
- Fully Connected Neural Network

#### Max Pooling:
- We generally use stride of 2 and kernel size of 2 -> Quartered size
- For all inputs within the kernel, take the MAX value and assign that to the kernel.
- Lets say we have 2 feature maps from 2 filters:
![[Pasted image 20251223211344.png]]
Red would be (3,0,3,1) in a 2x2 square. 
- Pooling makes the representation more compact
- Also allows it to be computationally more managable as the network goes deeper.

After each "Convolution" and "Max Pooling" step, we get a new image! WOAH! 

#### Flattening:
Literally spaghetti that bih. Imagine youre reading it, left to right top to bottom for the first map, then second then third (if one exists) then ... etc
Then feed it into the FCNN!
- Make sure the number of neurons coming out of the last layer is the number of classes in the dataset

#### SoftMAX
- The output from something like ReLu (Rectified linear unit) cant be considered probability
- To interpret raw classifier scores as probabilities, we want to use the Softmax classifier!
	- Converts a vector of raw scores into probabilities by:
		- Exponentiating each score
			- AKA take "e" and power it to each potential.
			- e as in eulers number!!
		- Normalising it
			- Then normalise em

#### Disadvantages of fully connected neural networks
- Non-localised features
- Many parameters to learn
- It doesnt scale well as LOTS of hidden layers
- Also takes data in as a vector so loses structural data

#### CNNs: 
- The filter kernel identifies the features within a receptive region of input
- The convolution later generates a feature map of the input layer
- Pooling - Reduces the resolution and generalises feature maps
	- Can do max, min or mean pooling however max is most expressive usually

- Convolution:
	- Visualise convolutional features
		- Low level feature -> Mid level -> High level feature -> Trainable classifier

REMEMBER:
- Values in a kernel are not predetermined but are learned through backwards propagation and gradient descent

