# Andrew_NG_ML

`
Code link - https://colab.research.google.com/drive/1jNVg0pSU5nNKY92FXyy9A0-JoBYsUaG_#scrollTo=Dc227tYUkHYp

`
## Most Common libraries used in sklearn
```python
# for building linear regression models and preparing data
from sklearn.linear_model import LinearRegression
from sklearn.preprocessing import StandardScaler, PolynomialFeatures
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error
```
### Spliting the data using sklearn
```python
# Get 60% of the dataset as the training set. Put the remaining 40% in temporary variables: x_ and y_.
x_train, x_, y_train, y_ = train_test_split(x, y, test_size=0.40, random_state=1)

# Split the 40% subset above into two: one half for cross validation and the other for the test set
x_cv, x_test, y_cv, y_test = train_test_split(x_, y_, test_size=0.50, random_state=1)

# Delete temporary variables
del x_, y_

```
### Normalising the training data using StandardScaler
```python
# Initialize the class
scaler_linear = StandardScaler()

# Compute the mean and standard deviation of the training set then transform it
X_train_scaled = scaler_linear.fit_transform(x_train)
```

## Most common libraries used in Tensorflow
```python
import tensorflow as tf
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
from tensorflow.keras.activations import linear, relu, sigmoid
from tensorflow.keras.losses import SparseCategoricalCrossentropy, BinaryCrossentropy
```
### Used for normalisation
```python
norm_l = tf.keras.layers.Normalization(axis=-1) # (100,2) -> (axis0,axis1) -> axis = -1 means last axis i.e. axis = 1
norm_l.adapt(X)  # learns mean, variance
Xn = norm_l(X)
```

### Creating a basic tf Sequential model
```python
model = Sequential(
    [
    tf.keras.Input(shape = (2,)),
    Dense(3,activation='sigmoid',name = 'layer1'),
    Dense(1,activation='sigmoid',name = 'layer2')
]
)

```
### Running the epochs on created model
```Python
# Say our input  features is of shape (200000,2) , it will convert in batches and then run, as it is not possible to run all the inputs at once.
model.compile(
    loss = tf.keras.losses.BinaryCrossentropy(),
    optimizer = tf.keras.optimizers.Adam(learning_rate=0.01),
)

model.fit(
    Xt,Yt,            
    epochs=10,
)
```

## Commonly used activation functions

<img width="931" height="319" alt="image" src="https://github.com/user-attachments/assets/ac98ddc7-9170-485b-afe5-5c98e90aabac" />

                    z = wx+b  


### 1. Sigmoid function    
Mostly used for Binary Classification.  

                    f(z) = 1/(1+e**(-z))

### 2. ReLU function
Used for Regression and Hidden layers

                    f(z) = max(0,z)

### 3. Linear activation function
Used for Regression

                    f(z) = z  ---> Basically no activation function used

### 4. Softmax function
It used for classification of more than 2 objects.  


$$
\text{Softmax}(z_i) = \frac{e^{z_i}}{\sum_{j=1}^{n} e^{z_j}}
$$

## Why Activation functions are needed ?
Say we use a very simple neural network, with **Liner activation function**.   
The output of first layer is passed onto 2nd, which still results in Linear output.  
So it is better to use **ReLU** for hidden layers (earlier sigmoid was used but ReLU is more fast and efficent).  

<img width="1838" height="663" alt="image" src="https://github.com/user-attachments/assets/c93bc817-3a80-40c0-ac81-9385800a215a" />

### Two approaches for Multiclassification
**1. Using Softmax**

We are applying softmax at the output of the final layer, the issue with this is that we are not able to compute the exact loss in next step.  
As we shold ideally calculate loss by comparing y and y^ , but in this case we are applying softmax to y^, which will not converge faster.
```python
model = Sequential(
    [ 
        Dense(25, activation = 'relu'),
        Dense(15, activation = 'relu'),
        Dense(4, activation = 'softmax')    # < softmax activation here
    ]
)
model.compile(
    loss=tf.keras.losses.SparseCategoricalCrossentropy(),
    optimizer=tf.keras.optimizers.Adam(0.001),
)

model.fit(
    X_train,y_train,
    epochs=10
)
```
**2. Using Logits**

In this case we will use the outputs as **Linear** from the final output layer.
After the model is trained, during prediction we can use softmax to the ouput of this model to convert it into probabilities.
```python
preferred_model = Sequential(
    [ 
        Dense(25, activation = 'relu'),
        Dense(15, activation = 'relu'),
        Dense(4, activation = 'linear')   #<-- Note
    ]
)
preferred_model.compile(
    loss=tf.keras.losses.SparseCategoricalCrossentropy(from_logits=True),  #<-- Note
    optimizer=tf.keras.optimizers.Adam(0.001),
)

preferred_model.fit(
    X_train,y_train,
    epochs=10
)
```
## Convolution Neural Network

Earlier we were using **Dense** layer, where all the inputs were interconnected to **all** the hidden layer units.  
But in case of **CNN**, we need not interconnect all the input layers to **all** the hidden units.  
We can decide, which inputs will map to which hidden layer units.

<img width="1840" height="562" alt="image" src="https://github.com/user-attachments/assets/a7670084-2845-416b-af51-fb4ae39fb675" />

### Why is this helpful ?

1. We can get better output even if we have less data.
2. Chances of overfitting are reduced. 

## Tradeoff between Bias and Variance

A example showing how bias and variance are impacted on the basis of degree of polynmial(no. of features, x)   
and what is the impact on cost function (J)

<img width="970" height="473" alt="image" src="https://github.com/user-attachments/assets/7788b5d5-e70b-4248-9c24-2e5f7d7e1313" />

The take away from this is that  
1. Use a larger neural network (with more hidden layers), this will lead to overfitting of training set.
2. Once we get a J for training set very low, then check the model against cv set.
3. If gap between cv and train set is high, add regularisation (lambda).

## Error Metrics

### Confusion matrix

We can use **Confusion matrix** to determine, the error and correct predictions.

<img width="1697" height="782" alt="image" src="https://github.com/user-attachments/assets/96f81ed3-cd63-4e29-8644-599d95069d6f" />

### F1 score
We cannot take average of presicion and recall when comparing different models, so F1 score gives better idea.

$$
F1 = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}
$$
