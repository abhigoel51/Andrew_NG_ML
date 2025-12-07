# Andrew_NG_ML

`
Code link - https://colab.research.google.com/drive/1jNVg0pSU5nNKY92FXyy9A0-JoBYsUaG_#scrollTo=Dc227tYUkHYp
`
## Most common libraries used in Tensorflow
```python
import tensorflow as tf
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
from tensorflow.keras.activations import linear, relu, sigmoid
```
## Used for normalisation
```python
norm_l = tf.keras.layers.Normalization(axis=-1) # (100,2) -> (axis0,axis1) -> axis = -1 means last axis i.e. axis = 1
norm_l.adapt(X)  # learns mean, variance
Xn = norm_l(X)
```

## Creating a basic tf Sequential model
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
