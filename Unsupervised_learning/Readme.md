# Unsupervised learning

## K-means clustering

1. Assign random clustering centroids.
2. Assign each input (x1,x2--,xn), to its closest centroid.
3. Take the mean of the input assigned, the clustering centroid will move in a certain direction.
4. Now repeat step 2 and 3, until clustering centroid does not move.
5. In this example 2 clusters will form, helping in classification of 2 groups.

<img width="1087" height="722" alt="image" src="https://github.com/user-attachments/assets/cda8ec6c-9a79-4de6-b986-0ef922c7f449" />


## Cost function for minimizing K-means

1. Assuming we have 2 clusters (it can be k), c(i) is used to map x(i) input into a cluster i.e. 1 or 2.
2.  Now we know c(i),μ_c(i) is the corresponding cluster centroid. This helps in calculating Cost function as shown below.

<img width="1283" height="781" alt="image" src="https://github.com/user-attachments/assets/f0202373-428e-4d75-aedf-5fabe5f3e2cb" />
