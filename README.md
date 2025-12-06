# Andrew_NG_ML

## Most common libraries used in Tensorflow
```python
import tensorflow as tf
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
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
