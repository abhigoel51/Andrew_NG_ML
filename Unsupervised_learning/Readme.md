# Unsupervised learning

## K-means clustering

1. Assign random clustering centroids.
2. Assign each input (x1,x2--,xn), to its closest centroid.
3. Take the mean of the input assigned, the clustering centroid will move in a certain direction.
4. Now repeat step 2 and 3, until clustering centroid does not move.
5. In this example 2 clusters will form, helping in classification of 2 groups.

<img width="787" height="422" alt="image" src="https://github.com/user-attachments/assets/cda8ec6c-9a79-4de6-b986-0ef922c7f449" />


## Cost function for minimizing K-means

1. Assuming we have 2 clusters (it can be k), c(i) is used to map x(i) input into a cluster i.e. 1 or 2.
2.  Now we know c(i),μ_c(i) is the corresponding cluster centroid. This helps in calculating Cost function as shown below.

<img width="783" height="481" alt="image" src="https://github.com/user-attachments/assets/f0202373-428e-4d75-aedf-5fabe5f3e2cb" />

## Anamoly detection
### Density estimation

We are considering 2 features for m different examples as shown  below.  
Say we plot a $$(m+1)^{\text{th}}$$ example with same 2 features, we will calculate the probabilty. If it is less then epsilon,   
then it is a anamoly.

<img width="1592" height="746" alt="image" src="https://github.com/user-attachments/assets/be0b2cc7-6f85-40da-9f69-3131b32eb12c" />

### Gaussian distribution

We can calculate probability of a feature, higher the probability, lower are the chances of it being anamolous and vice versa.  

$$f(x) = \frac{1}{\sigma \sqrt{2\pi}} e^{-\frac{(x - \mu)^2}{2\sigma^2}}$$

<img width="423" height="272" alt="image" src="https://github.com/user-attachments/assets/29c625ee-c94c-4ff2-bebd-4dfb78e0bf6e" />

Below is example for just **1 feature set** for m examples.  
We need to calculate mean and variance from the feature set of m examples.

<img width="545" height="329" alt="image" src="https://github.com/user-attachments/assets/ec0bde3c-1359-4eee-a056-825415a50315" />

So basically in this example we are choosing n features for m examples of x_i, those can help in detecting anamoly (n features).  

<img width="1333" height="758" alt="image" src="https://github.com/user-attachments/assets/2298421e-5042-479b-8e3c-15fa81f3fc0d" />

**Why this works ?**  
We are calculating probability for a given example accross n features and multiplying them (to calculate the chances of occurence of that event). Say for any $$(n)^{\text{th}}$$ feature, probability is very low or high then this will point to anomly as output probability will reduce or increase drastically because of multiplication.

A example for 2 features

<img width="1316" height="788" alt="image" src="https://github.com/user-attachments/assets/540fa3e4-16fd-4551-9ad7-f7fd39db2f70" />

We are considering 2 examples $$x^1$$ and $$x^2$$ , with 2 features x_1 and x_2.  
In case of $$x^2$$ probability is less than epsilon, so it can be a anamoly.

#### How to choose features for anamoly detection ?

1. Choose **Gaussian features** - Say i have feature x_1, which is non-gaussian, if i can make the distribution gaussian by transforming        x_1 by taking log(x_1) or x_1**0.5 etc then this is a better choice.
2. Introduce new features by combining already existing features.

<font color="Red">Note:  
1. Anamoly detection is used when most of the data points are working as expected and only few data points are not working as expected.
2. It is also used when the future input features can change unlike in case of supervised learning. For e.g. if we map proability distribution using 2 features i.e heat and vibration in case of airplane engines, but in future the input features change. But we still expect anamoly detection to work. 

