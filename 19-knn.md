Here, we are going to try 
 - split sample
 - run regression
 - apply a decision rule
 - apply to new data
 - examine the confusion matrix and ROC curve.

In this section, I rely in part on https://lgatto.github.io/IntroMachineLearningWithR/supervised-learning.html#model-performance (particularly for the discussion of k-nearest neighbor analysis).
```
## Another approach: k-nearest neighbor

In the discussion of @stephens2017everybody, we considered prediction by "doppelgangers." Here we will try k-nearest neighbor analysis - if a person is most like someone else in the dataset who has had an affair, we predict an affair, else not.

This approach is akin to reasoning by analogy, rather than by induction. (*I won't go out with Fred because he reminds me of Willie who was a cad/jerk/player/etc.*)

To run this, we need three inputs: our predictors in the training data, our predictors in the test data, and our outcome/classes in the training data.

unlike the lm and glm commands, knn will not automatically create our dummy variables for us. so we need to do this manually.

​```{r KNN0414}
library(class)
trainFair$sexMale <- ifelse(trainFair$sex == "female", 0, 1)
testFair$sexMale <- ifelse(testFair$sex == "female", 0, 1)
trainFair$childyes <- ifelse(trainFair$child == "no", 0, 1)
testFair$childyes <- ifelse(testFair$child == "no", 0, 1)

knnAffair <- knn(trainFair[,c(2,3,5:8,10:11)], 
                 testFair[,c(2,3,5:8,10:11)],
                 trainFair$affairYN
                 )
#head(knnAffair)
#summary(knnAffair)
confusionMatrix(knnAffair, testFair$affairYN)
```

### From 1 doppelganger to many

In the above, we have used a k-nearest neighbor analysis with the default value of k - which is 1.  What happens to prediction if we change this?

We can extend knn to cases where we are predicting not just a dichotomous outcome, but a multinomial one - such as the MBTI types and attachment classifications that students in class are working on.

```

```