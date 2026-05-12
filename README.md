import backtrader as bt

class MyStrategy(bt.Strategy):
    def __init__(self):
        self.sma = bt.indicators.SimpleMovingAverage(period=20)

    def next(self):
        if self.data.close > self.sma:
            self.buy()
        elif self.data.close < self.sma:
            self.sell()

# Setup Backtest
cerebro = bt.Cerebro()
cerebro.addstrategy(MyStrategy)
# Yahan apna data load karein
# cerebro.run()
import ccxt
import time

# Connection Setup
exchange = ccxt.primexbt({
    'apiKey': 'YOUR_API_KEY',
    'secret': 'YOUR_SECRET_KEY',
    'enableRateLimit': True,
})

def execute_trade(symbol, side, amount):
    try:
        order = exchange.create_order(symbol, 'market', side, amount)
        print(f"Order Executed: {order}")
    except Exception as e:
        print(f"Error: {e}")

# Example Loop
while True:
    # Yahan apni strategy logic lagayein
    # price = exchange.fetch_ticker('BTC/USD')['last']
    # if condition: execute_trade('BTC/USD', 'buy', 0.01)
    time.sleep(60)
