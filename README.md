# Prediction-Assignment-Writeup-

library(caret)

data <- read.csv("pml-training.csv")
valid <- read.csv("pml-testing.csv")

inTrain <- createDataPartition(y=data$classe,
                               p=0.7, list=FALSE)
training <- data[inTrain,]
testing <- data[-inTrain,]
dim(training); dim(testing)

columns <- c(8:11, 37:49,60:68,84:86, 102, 113:124,140,151:160)
training <- training[,columns]
testing <- testing[,columns]

# Running the model 

set.seed(757)
cv <- trainControl(method="cv", number=3)
modFit <- train(classe~.,data=training, method="rf", trControl=cv, verbose=F)

prediction_rf <- predict(modFitRf,newdata=testing)
confusionMatrix(prediction_rf,testing$classe)


