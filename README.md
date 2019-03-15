# For complete documentation please refer to the report.


### Approach to solve this recommendation problem:

  - **Implicit latent feature learning based models (Unsupervised)**
  To fill the ratings matrix, there are traditional matrix-factorization based methods like singular value decomposition and non-matrix-factorization methods like ratings prediction based on the cosine similarity between restaurants (or users). In this methods, the models implicitly learns the latent features of the users and restaurants and use them to predict the unseen ratings.

  - **Singular Value Decomposition**
The singular value decomposition helps to get a low-rank approximation of the ratings matrix. This lowrank approximated matrix is not sparse like the ratings matrix and predicts the previously unseen ratings that might be given by a user to a restaurant.
  - **Cosine Similarity Based Prediction**
  Another traditional approach to predict unseen ratings for a restaurant is by comparing the restaurant (the user) to other similar restaurants (users) in the data set and inferring the ratings based on the ratings given the similar restaurants (users).
  - **Explicit latent features learning based models (Supervised)**
 We estimate the similarity between the restaurants (users) using the cosine similarity. Some modifications to this approach is to correct the ratings matrix for the restaurant (user) biases before finding the similar restaurants (users).
*In this project, the singular value decomposition and cosine-similarity based ratings predictions would act as the baseline models.*
  - **Latent Features Learning using Alternating Least Squares (ALS) Method**
  In the ALS method, each user is represented by a k-dimensional feature vector where each dimension represents an attribute of the user which is latent. Similarly, each restaurant is also represented using a k-dimensional vector containing k latent features describing the restaurant. These features are learnt by the model and are parameters of the model. Hence, the data instance will be a randomly initialized k-dimensional vector representing the user xi, a randomly initialized k-dimensional vector representing the restaurant yj, the rating given by the user to the restaurant 𝑟𝑖𝑗. The target variable is 𝑟𝑖𝑗. The function that predicts rij from xi, yj is a simple dot product between the feature vectors. The loss function will be a mean square loss with L2 regularization on xi, yj since they are the parameters of our model. Given this setup, we can find all xi’s and yj’s and fill the matrix as a typical supervised learning problem.
  - **Latent Features Learning using Stochastic Gradient Descent (SGD) model**
  In the SGD model, the setting is similar to ALS where the latent feature for each user and restaurant is learned. In addition to ALS, there is an additional parameter that is learned for each user and restaurant. For each user and restaurant, a bias term is also learned. The intuition behind learning this bias term is many a times some user or restaurant tend to give / receive higher ratings on average as compared to others. So to ensure that the latent feature for each user and restaurant is free from such biases, it is learned as a separate parameter. Essentially, the final rating given by a user i to restaurant j is broken into four components: a global bias (average of all the available ratings), a user bias, a restaurant bias and a component dependent on the interaction between user i and restaurant j. To learn the parameters of the model (all the biases and latent feature vectors), stochastic gradient descent is used. Hence, it is called SGD model.
  - **Converting it into a Regression/Classification Problem**
 Using the latent features learned for each user and restaurant, the matrix completion problem can be converted to a regression or a classification problem that can be dealt with using powerful techniques like Random Forest Regressor, etc. In this project, we have tried with Random Forest Regressor.
- **Random Forest Regressor Based Model**
Random forest regressor tries to learn the non-linear dependency between the user latent vectors and restaurant latent vectors. The target variable is the rating given by user i to restaurant j. It essentially boils down to a regression problem.
**Evaluation Metric**
The evaluation metric used for comparing the different models is the mean square error (MSE). The mean square error is easy to interpret. The square root of MSE will give the error the recommendation engine makes while predicting an unknown rating. The lower MSE means the model has correctly learned the latent features that characterizes the user and restaurant which can be used by Yelp to generate insights and recommends new restaurants to users and new users to restaurants.
The model selection is based on the best out of sample MSE obtained for a model. The reasons for improvement in the MSE between different models are analyzed and documented in this report.
    


### Summary of the models:

Based on the analysis of all the models, we choose the Ensemble Model for both the Restaurants in Phoenix and for the Restaurants in Scottsdale as the best model for recommendation.
On testing the models on the Test Data, we got: MSE of 2.663 (for Restaurants in Phoenix) and 2.518 (for Restaurants in Scottsdale).

| Models | Phoenix | Scottsdale 
| ------ | ------ |---------|
| SVD    | 17.19524313333571 | 16.68550995321838
| Cosine Similarity based model | 16.68550995321838 | 17.025866680642704
| GALS based model | 17.230543322467152 | 16.729128335518105
| SGD based model| 17.230543322467152 | 2.7363082502586065
| Random Forest Regressor| 2.710045376922961 | 2.6717940609972395
| ***Ensemble of SGD and RF*** | **2.6333817860275097** | **2.5183558867860882**






[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)


   [dill]: <https://github.com/joemccann/dillinger>
   [git-repo-url]: <https://github.com/joemccann/dillinger.git>
   [john gruber]: <http://daringfireball.net>
   [df1]: <http://daringfireball.net/projects/markdown/>
   [markdown-it]: <https://github.com/markdown-it/markdown-it>
   [Ace Editor]: <http://ace.ajax.org>
   [node.js]: <http://nodejs.org>
   [Twitter Bootstrap]: <http://twitter.github.com/bootstrap/>
   [jQuery]: <http://jquery.com>
   [@tjholowaychuk]: <http://twitter.com/tjholowaychuk>
   [express]: <http://expressjs.com>
   [AngularJS]: <http://angularjs.org>
   [Gulp]: <http://gulpjs.com>

   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
   [PlMe]: <https://github.com/joemccann/dillinger/tree/master/plugins/medium/README.md>
   [PlGa]: <https://github.com/RahulHP/dillinger/blob/master/plugins/googleanalytics/README.md>
