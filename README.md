# Building Classifiers (binary and multiclass)

Classification: supervised learning algorithms with a categorical outcome.

## Logistic regression

Error metrics:
Accuracy is the total correct prediction over all of our labels.
$$accuracy = \frac{TP + TN}{TP + FN + TN + FP}$$

Recall is the meaure of the ability to identify all actual positive instances. The percentage of the actual postive positive instances we predicted well
$$recall/sensitivity = \frac{TP }{TP + FN}$$

From all predictions how many did we get right? that is answered with precision measure
$$precision = \frac{TP }{TP + FP}$$

Specificity is the meaure of the ability to identify all actual negative instances. The percentage of the actual negative instances we predicted well
$$specificity = \frac{TN }{TN + FP}$$

f1 score or harmonic mean
$$F1 = 2\frac{precision * recall}{precision + recall}$$

Receiver Operating Characteristics (ROC) ; plot of true positive rate (sensitivity) vs false positive rate (1- specificity). The ROC area under the curve is called AUC. The ROC curve is better for data with balanced classes and the precision-recall curve is better for unbalanced classes

## K Nearest Neighbours Classification

- correct value for K (it is a hyperparameter)
  - the right k depends on which error metric is most important
  - a common approach is to use an elbow method approach
  -
- How to measure closeness of neighbours

  - close points are thought to be similar
  - distances: euclidea distance (L2): $\sqrt{x^2+y^2}$ and Manhattan distance (L1): $|x|+|y|$
  - apply faeture scaling to ensure each feature has equal weights on the knn algorithm

- Pros:

  - simple to implement
  - adpats well as new training data is introduced
  - Easy to interpret

- Cons:
  - Slow to predict because of many distances to be calculated
  - Does not generate insight into data generating process (no model)
  - requires a lot of memory for large dataset (model has many parameters which will all have to stored)
  - KNN accuracy breaks down when there are many predictors, due to curse of dimensionality

# Support Vector Machine (SVM)

This is an extension support vector classifiers which finds a soft margin boundaries in the data based on cross validation (allows for some misclassification to make better predictions i.e. calculates hyperplanes that minimizes misclassification). They do not return predicted probabilities like in the logistic regression.

## Approach 1

- Start data in a relatively low dimension
- Increase the data into a higher dimension
- Find a support vector classifier that separates the higher dimensional data into two groups

## Approach 2:

Transform the space to a different coordinate system

## Extending SVM to non-linear classifiers using the kernel trick (SVM Gaussian Kernel)

- Under the right transformation of our space, we can find a linear separation hyperplane which maps back to our non-linear decision boundary
- SVMs with RBF kernels are very slow to train with lots of features or data. To address this we construct an approximmate kernel map with SGD using Nystroem or RBF sampler to create dataset in higher dimensional space and then fit a linear classifier.

Many features (~ 10K features) - small data (1k rows) - use simple logistic or LinearSVC

Few features (< 100 features) - medium data (~10k rows) - use SVC with RBF

Few features (< 100 features) - many data (100k rows) - Add features and do logistic reg, or use LinearSVC after kernel Approx
