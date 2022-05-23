# Recurrent Neural Networks; Tuning and Regularizing

## Random seed
Set numpy and tensorflow RNGs to generate numbers with a seed of "123" for easily repeatable results.
## Optimization metric
Import the appropriate metric that will be used for optimization (remember you are predicting a continuous, not categorical variable).
## Index the 'Month' column
Covert dates if necessary.
## Plot initial data
Check the trend for stationary signs (Dickey-Fuller test). The goal is constant variance (i.e. variance is not increasing/decreasing with time) and no trend in the data. If data proves to be non-stationary, correct for this problem (to correct for variance issues - log transform the data; for trend - take the first difference).
## Split data into test-training sets
Take the data from the very last year (1960) for the test set (i.e. the last 12 entries).
### Optional step
Create the index arrays for both train and test datasets. For example:

    train_idx = df.index <= train.index[-1]

## Sliding frame
Create the appropriate data structure for a time series analysis where the past 10 datapoints will be used to make predictions of the next 1 datapoint.
## Reshape data
Reshape the created dataframe into the 3D format that RNN expects.
## Generate layers
Create a one-layer LSTM with 25 units (neurons). Train it for 100 epochs with the default mini batch size of 32.
## Compile and fit the model
When compiling, specify the **sgd** optimizer, and choose an accuracy metric (e.g. **mse**, **mae**, **mape**, etc.) to judge the goodness of your predictions. To compare further on the prediction results with the true values in the test set, specify inside the fit function your validation data: validation_data = (X_test, y_test). Save the history of the loss and the accuracy results in each epoch as the model is being trained, to subsequently plot them and compare.
## Plot loss and accuracy values
Plot the loss and accuracy in each epoch for the training set as well as the validation set. Comment on results. Are there any signs of overfitting? Signs of vanishing or exploding gradient? Explain how the two would manifest in the graph. 
## Calculate predicted values
Compute the model predictions, undo the *differencing*, and plot the results.
## Tuning
1. Train the model for 500 epochs. Are your predictions better? Should you have stopped before the end of the 500 epochs judging by your loss and accuracy plots? If yes at what epoch would you stop and why?
2. Try two, three, and four  layers for your RNN with 50 and 100 neurons in each of the hidden layers (you should get altogether 6 models – 2 layers & 50 neurons, 2 layers & 100 neurons, 3 layers & 50 neurons, etc.). Train each of them for 100 epochs and save and plot the accuracies and the losses for each of the 6 combinations. Do you see signs of overfitting? Which model overfits most? Explain.
3. For the most severely overfitting model from the 6 options above use the Dropuot in combination with the L2 method, to regularize your overfitting model. Be creative, try different options to correct for the overfit.
4. Could you create a model that beats the first one (the one with 1 layer and 25 units) and is not overfitting after regularization was applied?
