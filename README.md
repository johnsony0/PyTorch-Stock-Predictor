# PyTorch-Stock-Predictor

This project aims to create a deep learning model capable of predicting the direction/value of stocks in the future. 

## Usage


### Prerequisites
All stock data is fetched using Alpaca API, you can get your own at their [website](https://alpaca.markets/) or this [guide](https://alpaca.markets/learn/connect-to-alpaca-api/). 

You may be prompted to enter your SSN as alpaca is also used for trading stocks, but you can close out of it, and use their key without needing to send them sensitive information. 

If you wish to use a different API such as vantage alpha or yahoo finance, you will just have to change the way the data is modified and saved into `self.data`.

### Running

This project was created using google colab, however it should be able to run on any IDE as well (such as VSCode) as long as your device supports python. If not using google colab, make sure to download all dependent libraries.

To start, import all libraries, run all functions, then call `main(ticker,lookback=15,lookforward=5,batch_size=1,num_epochs=5)` with required ticker input, and the rest are optional. Such an input can look like `main("AMZN",lookback=60,lookforward=20,batch_size=1,num_epochs=20)`.

### Training

The training set is the first 80% of the data. Training loop uses tqdm to approximate the time taken to train each epoch of data. Calculates and returns the MSE loss and correct direction percentage. Correct direction means if the model calculates the correct direction the stock goes (ex: up or down).  

![Training_Loop](https://github.com/johnsony0/Pytorch-Stock-Predictor/assets/76934261/9708d928-760c-4ad9-80fc-328e67c52b40)

Then it plots the training loss over epochs and directions percentage over epochs.

![Training_Graphs](https://github.com/johnsony0/Pytorch-Stock-Predictor/assets/76934261/a661f4ea-fb9e-46ae-972e-7708601dd2b1)

### Analysis

Generally the model works much better with more data. Alpaca historical stock data only has about 7 years of data, so using stocks that have >7 years of data is preferred, such stocks include 'IBM', 'NVDA', 'AMZN' while more recent stocks like 'RDDT' will not yield good results. 

When testing the model, we test it on the last 20% of the dataset. The normalized loss is calculated using MSE and the unnormalize loss is calcualted with manhatten distance. Since our y axis is aligned it is just the abs(label-predicted).

![Test_Loop](https://github.com/johnsony0/Pytorch-Stock-Predictor/assets/76934261/d649c5de-2580-4caa-aa9d-8d78515df14b)

Our first chart displays the entire history of the stock that we have data on, and the overlay of our prediction. Here we can see when trained and tested on AMZN historical data, it is able to map the test set pretty well.

![Predicted_Vs_Actual](https://github.com/johnsony0/Pytorch-Stock-Predictor/assets/76934261/f16f33ca-c6bf-4939-bfcf-c5d3222cf42b)

Our next chart displays the first chart but zoomed in specifically on the region that we predict. A quick analysis shows that in the beginning of 2023 the model consistently predicts the stock should be lower than it actually is (the Predicted is under the Actual line), meaning the model thinks the stock is overvalued and should drop. Later from mid 2023 to 2024, the model thinks the stock is undervalued and consistently predicts a value > than the actual value. Currently in mid 2024, it once again predicts the stock to fall, as with each input it always outputs a lower value. 

![ZoomedIn_Predicted_Vs_Actual](https://github.com/johnsony0/Pytorch-Stock-Predictor/assets/76934261/42bb0c9b-2e5d-41f6-a226-c3baa0da0bfd)

The last chart diplays the future predictions. Through testing I noticed the model is not very good at predicting the actual value of future trading days, however it does do well in predicting the overall direction and trend. For example in the graph before it correctly deduces when the stock was undervalued. In this graph it shows that the model believes AMZN will be bearish in the near future, although it is ridiculous to think that AMZN will drop 20 pts linearly in 20 days. 

![Future_Predictions](https://github.com/johnsony0/Pytorch-Stock-Predictor/assets/76934261/1e61ca7d-e6d1-42e7-abc5-46d586d7b4f5)

## Features

- Batch Inputs (make sure to add batch normlization to StockPredictionLSTM class), declare batch_size when calling main:
`main("META",lookback=60,lookforward=20,batch_size=1,num_epochs=20)`
- Expandable Features. Called within StockDataset.init, you can add more features to norm_data such as `norm_data = np.hstack((norm_close_prices, rsi, norm_volumes))`. Make sure the first index of each array is the close price. Also the new features should all be normalized using a unique MinMaxScaler. Although if the feature is already a value between 0 and 1 such as rsi values, it does not need to be further normalized. A caveat to this is if there is only one feature then use `self.data  = {feature}` such as `self.data = norm_data`. The rest of the code should work as intended and should not have to be changed to account new features or removal of features. 
- Extensive Data Collection + Output
- GPU Support 

## Model

Stocks are a time-series dataset, so using a RNN is a logical choice. LSTMs does not suffer from a regular RNN's vanishing gradient problem, and is often better at handling sequential data than RNNs.

The model consists of 2 LSTM layers, followers by 1 fc layer
![model](https://github.com/johnsony0/Pytorch-Stock-Predictor/assets/76934261/508f589a-7ee9-44ad-87e4-a364d0eb346f)

## Future Work

- Improve model
- Custom LSTM
- Output dates in the future predictions array
- Better predictor of value
- GPU processing capabilities

## Contributing

The project is not optimized but provides a great foundation. All the tools for data is already implemented (loss graph, prediction vs actual graph, future predictions graph, etc), however feel free to tweak anything.
Such as but not limited to adding new features, remove features, test different batch inputs, epochs inputs, models, layer sizes, optimizers, loss functions, etc. 

Pull requests are welcome. 

For suggestions feel free to send me an email from [my website](https://johnsony0.github.io/contact). 

Likewise for bugs/errors, or report it as an issue. 

Feel free to use this code, but please give credits.

Thanks :D
