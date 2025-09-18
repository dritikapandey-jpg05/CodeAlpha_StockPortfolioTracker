# CodeAlpha_StockPortfolioTracker
stock_prices = {"AAPL": 180, "TSLA": 250, "GOOGL": 130, "MSFT": 280}

def main():
    portfolio = {}
    print("Enter your stock holdings (type 'done' to finish):")
    
    while True:
        stock = input("Enter stock symbol: ").upper()
        if stock == 'DONE':
            break
        if stock not in stock_prices:
            print(f"Stock '{stock}' not found. Available stocks: {list(stock_prices.keys())}")
            continue
        
        try:
            quantity = int(input(f"Enter quantity for {stock}: "))
            if quantity < 0:
                print("Quantity can't be negative. Try again.")
                continue
        except ValueError:
            print("Invalid input for quantity. Please enter an integer.")
            continue
        
        if stock in portfolio:
            portfolio[stock] += quantity
        else:
            portfolio[stock] = quantity

    total_investment = sum(stock_prices[s] * q for s, q in portfolio.items())

    print("\nYour Portfolio:")
    for s, q in portfolio.items():
        print(f"{s}: {q} shares x ${stock_prices[s]} = ${stock_prices[s]*q}")
    print(f"Total Investment Value: ${total_investment}")

    save = input("Do you want to save the portfolio to a file? (y/n): ").lower()
    if save == 'y':
        filename = input("Enter filename (e.g., portfolio.csv): ")
        try:
            with open(filename, 'w') as f:
                f.write("Stock,Quantity,Price,Value\n")
                for s, q in portfolio.items():
                    value = stock_prices[s]*q
                    f.write(f"{s},{q},{stock_prices[s]},{value}\n")
                f.write(f"Total,,,{total_investment}\n")
            print(f"Portfolio saved to {filename}")
        except Exception as e:
            print(f"Failed to save file: {e}")

if __name__ == '__main__':
    main()
