# Grapefruit and Orange Predictor


# Models AUC:
Neural Network: 0.92 <br/>
Random Forest: 0.965 <br/>
Stacked: 0.98 <br/>

# Project Report

The basis of this project is to predict given a set of certain attributes whether the given fruit is an orange or a grapefruit. For my ensemble I decided to utilize two predictor models: convolutional neural network and a random forest. The designs of both the neural network and the random forest were constructed by my professor at the time. It was up to me to optimize the hyperparameters of both models. Additionally, I had to pick what models we wanted to include out of the many binary prediction models made available to us. 

For the neural net implementation, I decided to train it using all of the features. Separating the data based on discrete features or binary features does not provide any improvement when training the neural net. The neural net was trained using the mltools package provided by my professor. I had it learn on our training data and checked the performance of the model with our validation data. Some key parameters that were set was only using one hidden layer which had 100 nodes within that hidden layer. Performing various testing I found that more nodes did not give equal better performance and more layers usually worsened the model’s performance. Then when setting the activation feature, I decided to use a logistic function as that one provides the smoothest curve. Some of the last hyper parameters we set was the stoptol and stepsize. The parameters were set this way so it would take smaller steps and not stop immediately. I wanted the neural net to run as many iterations as it could without stopping early.

The random forest was constructed with thirty individual decision trees. This inherently reduces how bias our predictions are on the validation data, test data, and computational cost. Each individual tree was initialized with parameters in which were optimized to keep from overfitting the training data. The process we used to find the best value for each parameter was by computing and plotting the training and validation error rates of a chosen range of values. From there we used our own intuition to determine what values provided the best decision tree. Bootstrapping was utilized in order to choose the random sample to be learned from each tree. A random sample size of the number of columns in the training data set with replacement was pulled for each decision tree to be trained on. We made sure the number of times we bootstrapped the data was sufficient enough to ensure that the whole population of the training data was covered.

In order to export the final predictions to Kaggle easier, a function was made to easily convert the predictions of each model to a csv file.  Each individual model’s test and validation predictions were stored in separate csv files. After each model’s predictions was collected for the test and validation data set, they were all horizontally stacked together. With the horizontally stacked validation predictions I trained a linear classifier in order to make predictions based off the horizontally stacked test predictions. A linear classifier was used since we found utilizing nonlinear classifiers did not significantly improve the results of the test predictions. A slight change in performance between a linear and nonlinear classifier showed me that the data set is linearly separable. So, with this known I chose to stick with a linear classifier in order to lower overall model complexity.

As discussed, I chose to investigate a neural network model, random forest decision tree model, and simple linear classifier. I expected my neural network to perform better, though its performance could be due to the length of time the algorithm was run. However, since we made the model run on smaller steps, this would have taken a long time to find a better model. In contrast, the random forest model could be overfitting, which could explain its higher AUC score. Overall, for the set of data provided, the random forest model was the best individual model. However, after combining the models, the stacked model of all three algorithms proved to perform better than the random forest model. 

