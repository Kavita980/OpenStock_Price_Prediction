# OpenStock_Price_Prediction

So, in this problem I had to use RNNs to try to predict the opening stock price based on last 3 days Open, High, Low prices and volume. So, the very first step in solving this problem was to create a new dataset which contains 12 features (last 3 days Open, High, Low price and volume values) and the target value is nothing but the next day’s Opening price value which we are trying to predict.

How I created the dataset : First of all I am going to input the q2_dataset and going to select the important columns which contains Open, High, Low price & volume values. After that I am going to create two X & y empty lists. I will create a loop which runs from 3 to 1259 (length of the dataset). Inside the loop I will select 3 days values in a 2d array. I am creating another loop which will convert the 2d array of 4*3 (last 3 days values) to 1d array which contains 12 feature values. After obtaining the 12 value array I will append that data into my X list. In the y list (target value) I will append the next day’s Opening value. And after the loop is over I will have new dataset’s X and y.

Then after obtaining the X & y I will split the dataset into 70-30 train test split randomly using train_test_split of the sklearn library. After obtaining the train & test dataset I will save the Train dataset into a file named train_data_RNN.csv, and I will save the test dataset into a file named test_data_RNN.csv. So, this is how I obtained the Train & Test dataset and saved it into Train_data_RNN.csv & Test_data_RNN.csv file.

Pre-processing steps taken: For training the model I will first import the train_data_RNN.csv file using pd.read_csv. After obtaining the dataset I will select the important columns using iloc command of the python. The feature values are in different range so I am using min max scaling to scale all the values between 0 and 1. It will make things faster and all the values will be in the same scale so it will help us predict better. We will be using the same min max scaling for test dataset too. So, first we will fit & transform the min max scaling on the train dataset then we will save the scaling model in the pickle file to use it with Test dataset as we should use the same scaling with test dataset too.

How I came up with the best Neural Network model: To obtain the best NN model I first started writing code for LSTMs using tensorflow. In the beginning I added 4 LSTM layers without overfitting each LSTMs had 128 units in them the result was good, the output prediction was close to the real value. But, when I found the MSE on the y_test & y_test_predicted then the MSE was near 80, this MSE was calculated after performing inverse transform on the predicted dataset.

I tried many different architecture I increased the depth of the model. I also added the dropout layer after each layer. I replaced LSTM with GRU layer. I found that GRU out performed LSTM really easily. I received 18.42 of MSE.

Above you will find the code which was able to obtain very low MSE.
