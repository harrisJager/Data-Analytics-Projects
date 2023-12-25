# Decision Tree Modeling using Penguin Dataset, rpart, making predictions and using confusion matrix to check predictions.

## Author
Harris Rizwan

## Date
2023-12-22

## Objective
This project focuses on building a decision tree model to predict the gender of penguins using the penguin dataset. The code involves data loading, preprocessing, model training, visualization, and prediction.

This R code performs decision tree modeling on a penguin dataset to predict the gender of penguins based on various features. Below is a step-by-step overview of the code:

Loading Data:

Installs and loads necessary R packages, including 'caret' and 'rpart.plot.'
Reads the penguin dataset from a CSV file.
Data Preprocessing:

Removes unnecessary columns, specifically 'IndividualID,' to prepare the data for modeling.
Performs one-hot encoding on categorical variables ('Species' and 'Island') using model.matrix.
Combines the one-hot-encoded matrix with the original dataframe.
Removes the original categorical columns.
Model Training:

Sets up a 10-fold cross-validation strategy using the 'caret' package.
Creates a decision tree model using the 'rpart' method and the specified training control.
Summarizes the model, displaying variable names and additional information.
Visualization:

Utilizes 'rpart.plot' to visualize the structure of the decision tree.
Model Evaluation:

Converts the 'Gender' variable to a factor for accurate evaluation.
Generates a confusion matrix to assess the accuracy of the model on the training data.
Predictions:

Reads the original dataset again to predict the gender using the trained model.
Performs one-hot encoding and necessary data preparation on the new data.
Uses the trained model to make predictions on the new data.
Result Presentation:

Combines the original dataset without the 'Gender' variable with the predicted values.
Renames the predicted column to 'Gender.'
Displays the first few rows of the resulting dataframe.
This code provides a comprehensive walkthrough of the process of training a decision tree model for gender prediction on the penguin dataset. It covers data loading, preprocessing, model training, visualization, evaluation, and result presentation in a clear and structured manner. Users can follow the code sequentially to understand and replicate the decision tree modeling process in their own R environment.



## Dependencies
Make sure to install the required R packages before running the code:

```R
install.packages('caret')
install.packages('rpart.plot')

library(caret)

Loading Data

data <- read.csv2("YourDirectory\\PenguinsWithoutMissingValues.csv")
head(data)

Preprocessing

df1 = subset(data, select = -c(IndividualID))

cols_to_encode <- c("Species", "Island")

# Perform one-hot encoding
one_hot_encoded <- model.matrix(~.-1 + ., data = df1[, cols_to_encode])

# Combine the one-hot-encoded matrix with the original dataframe
df1 <- cbind(df1, one_hot_encoded)

# Remove the original categorical columns
df1 <- df1[, !names(df1) %in% cols_to_encode]
df1

Model Training

ctrl <- trainControl(method = "cv", number = 10, savePredictions = TRUE)

model <- train(Gender ~ ., data = df1, method = "rpart", trControl = ctrl)

# Visualize the best model using rpart.plot
library(rpart.plot)
rpart.plot(model$finalModel)

Model Evaluation

df1$Gender <- factor(df1$Gender)

conf_matrix <- confusionMatrix(predict(model, newdata = df1), df1$Gender)
print(conf_matrix)

Making Predictions

df1 <- read.csv2("YourDirectory\\PenguinsWithoutMissingValues.csv")

cols_to_encode <- c("Species", "Island")
df1 = subset(df1, select = -c(IndividualID))

# Perform one-hot encoding
one_hot_encoded <- model.matrix(~.-1 + ., data = df1[, cols_to_encode])

# Combine the one-hot-encoded matrix with the original dataframe
df1 <- cbind(df1, one_hot_encoded)

# Remove the original categorical columns
df1 <- df1[, !names(df1) %in% cols_to_encode]
df1

Making Predictions

# Use the trained model to make predictions on the new data
predictions <- predict(model, newdata = df1)

# Print or use the predictions as needed
print(predictions)

Adding Predicted Values to the DataFrame

df1 = subset(data2, select = -c(Gender))

combined_df <- cbind(df1, predictions)

# Renaming predictions to Gender
colnames(combined_df)[colnames(combined_df) == "predictions"] <- "Gender"

head(combined_df)
