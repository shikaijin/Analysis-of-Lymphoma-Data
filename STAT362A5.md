```
library(class)
library(tidyverse)
library(C50)
```

Q1(a): Perform the min-max normalization on the two datasets iris_train.csv and iris_test.csv.\
Q1(b): Perform the k-nearest neighbour classification using knn from the package class with k = 3.\
Q1(c): Find out the testing accuracy in Q1(b).\
Q1(d): Type ?knn and read the documentation for knn(). What is the use of prob in the function? Now,
set the argument prob = TRUE and redo Q1(b).
```
# Q1
iris_train <- read.csv("C:/Users/ROG/Desktop/iris_train.csv")
iris_test <- read.csv("C:/Users/ROG/Desktop/iris_test.csv")

# Q1(a)
iris_train2 <- iris_train[, -5]
iris_test2 <- iris_test[, -5]

iris_train_n <- iris_train2
iris_test_n <- iris_test2

train_min <- apply(iris_train2, 2, min)
train_max <- apply(iris_train2, 2, max)

for (i in 1:ncol(iris_train2)) {
  iris_train_n[, i] <- (iris_train2[, i] - train_min[i]) / (train_max[i] - train_min[i]) 
  iris_test_n[, i] <- (iris_test2[, i] - train_min[i]) / (train_max[i] - train_min[i]) 
}



# Q1(b)
iris_train_labels <- iris_train$Species
iris_test_labels <- iris_test$Species

knn_predicted <- knn(train = iris_train_n, test = iris_test_n, cl = iris_train_labels, k = 3)


# Q1(c)
tb1 <- table(iris_test_labels, knn_predicted)
##                knn_predicted
## iris_test_labels setosa versicolor virginica
## setosa         15          0         0
## versicolor      0         16         2
## virginica       0          1        16

accuracy <- sum(diag(tb1)) / length(iris_test_labels)
## [1] 0.94


# Q1(d)
# The prob argument in knn() determines if the proportion of the votes for the winning class are returned as attribute prob.
# If prob = TRUE, the percentage of votes for the winning class is returned in the form of attribute prob.

knn_predicted2 <- knn(train = iris_train_n, test = iris_test_n, cl = iris_train_labels, k = 3, prob = TRUE)

```



Q2: Write a function called knn_L1 that performs k-nearest neighbour classification using the L1-norm. 
Your inputs are train, test, cl, k, where train is your training dataset, test is your testing dataset, cl
is your true classifications of training set, and k is the number of neighbours considered.
Your output should be a list with two elements. The first element is called class, which contains the
predicted class labels. The second element is called prob, which contains the proportion of the winning vote.
```
knn_L1 <- function(train, test, cl, k){
  class <- rep(0, nrow(test))
  prob <- rep(0, nrow(test))
  n <- apply(matrix(unlist(train), nrow = nrow(train), ncol = ncol(train)), 2, as.numeric)
  
  for(j in 1:nrow(test)){
    m <- apply(matrix(test[j,], nrow = nrow(train), ncol = ncol(test), byrow = TRUE), 2, as.numeric)
    d <- rowSums(abs(n - m))
    tb <- tibble("L1" = d, "label" = cl) %>% 
      arrange(L1) %>% 
      filter(L1 <= L1[k])
    result <- as.data.frame(prop.table(table(tb$label)))
    class[j] <- knitr::combine_words(as.character(result$Var1[result$Freq == max(result$Freq)]), and = ", ")
    prob[j] <- max(result$Freq)
  }
  list(class = class, prob = prob)
}
```

Q3: Redo Q1(b) and Q1(c) with your function in Q2.
```
knn_L1predicted <- knn_L1(train = iris_train_n, test = iris_test_n, cl = iris_train_labels, k = 3)
tb2 <- table(iris_test_labels, knn_L1predicted$class)
##
## iris_test_labels setosa versicolor virginica
## setosa         15          0         0
## versicolor      0         16         2
## virginica       0          1        16
## 
accuracy2 <- sum(diag(tb2)) / length(iris_test_labels)
## [1] 0.94
```
