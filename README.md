# TradeXperto

Hi! I'm Federico, an Electronic Engineer and an algorithmic trader. When I was attending a subject at the university I made a project which uses a genetic algorithm to find the best parameters for a trading strategy. In that moment I realized that I was developing a noval framework for creating, testing and optimizing trading strategies based on classical rules or machine learning models. I decided to continue working on it and I created TradeXperto.

## Design
![TradeXperto Diagram](https://github.com/fedegonzalezit/tradexperto/assets/65198435/c0b350c8-5c56-4128-9cc6-afd6908bf1d1)

TradeXperto enables you to do the following:
- Define a set of rules that use technical indicators.
- Create your own technical indicators.
- Add your own features.
- Create a strategy to define stop loss and take profits.
- Create a strategy to size each trade.
- Optimize hyperparameters of strategies.
- Train machine learning models.

## How it works
### Creating a simple moving average strategy
First, import the module:

```python
from tradexperto_framework import TradeXperto
tx = TradeXperto()
```

Set the data source:
```python
tx.set_asset(asset="AAPL", api="yfinance")
```

After importing the module, you have to define the indicators that you will use:
```python
# If needed, you can compose indicators, using one indicator as an input for another.
tx.set_indicator("sma_slow", "sma", window=70)
tx.set_indicator("ema_fast", "ema", window=21)
```

Set the rules:
```python
tx.add_trigger("LONG_OPEN", "(ema_fast +cross sma_slow)")
tx.add_trigger("LONG_CLOSE", "(ema_fast -cross sma_slow)")

tx.add_trigger("SHORT_OPEN", "(ema_fast -cross sma_slow)")
tx.add_trigger("SHORT_CLOSE", "(ema_fast +cross sma_slow)")
```

You are done! Test the strategy:
```python
backtest_result = tx.backtest(
    money=10000,
    short_enable=True,
    long_enable=True,
    start="2010-01-05",
    end="2023-08-30",
    candle="1d",
)
backtest_result.plot(money=True)
```

For more examples, see the "examples" folder.

## Roadmap
Before creating TradeXperto, I developed several scripts that I'm integrating into this framework. For that reason, TradeXperto is not finished yet. This is the roadmap:

#### TradeXperto 1.0
| Feature                  | Developed | Integrated | Tested |
|--------------------------|----------------|----------------|---------------|
| Rules-based strategies   | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| yfinance integration     | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| CSV data integration     | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| Calculator of indicators | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| Backtest                 | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| Stop-loss and Take-profit | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| BetSizer                 | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| Portfolio of assets      | :white_check_mark: | :x: | :x: |
| Markowitz portfolio optimization | :white_check_mark: | :x: | :x: |
| Multiple assets and multiple strategies | :x: | :x: | :x: |
| Metatrader bot | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| Telegram alarm | :white_check_mark: | :x: | :x: |
| Binance bot | :x: | :x: | :x: |

#### TradeXperto 1.1
| Feature                  | Developed | Integrated | Tested |
|--------------------------|----------------|----------------|---------------|
| Fuzzy logic | :white_check_mark: | :x: | :x: |
| Brute Force Optimization | :white_check_mark: | :x: | :x: |
| GA Optimization | :white_check_mark: | :x: | :x: |

#### TradeXperto 1.2
| Feature                  | Developed | Integrated | Tested |
|--------------------------|----------------|----------------|---------------|
| ML Models | :x: | :x: | :x: |

