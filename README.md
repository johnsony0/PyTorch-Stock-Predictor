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

INSERT IMAGE OF TRAINING LOOP


### Analysis

Works better with more data so older stocks generally give better results. 
mention how to read plots (if predictions is under then the stock is overvalued we expect it should be lower, else undervalued should be higher)

Test Loop [Test_Loop.png]

Predicted vs Actual [predictedvsactual.png]

Zoomed in Predicted vs Actual[ZoomedInPredictedVsActual.png]

Future Predictions [futurepredictions.png] 

## Features

## Model

INSERT IMAGE OF MODEL [model.png]

## Future Work

- Improve model
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
