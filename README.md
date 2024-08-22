import requests
def get_exchange_rate(source, target):
    response = requests.get(f"(link unavailable)")
    data = response.json()
    return data["rates"][target]

def convert_currency(amount, source, target):
    exchange_rate = get_exchange_rate(source, target)
    converted_amount = amount * exchange_rate
    return converted_amount

def main():
    print("Currency Converter")
    currencies = ["USD", "EUR", "GBP", "JPY", "CNY", "INR"]
    while True:
        print("\nSelect source currency:")
        for i, currency in enumerate(currencies, start=1):
            print(f"{i}. {currency}")
        source_choice = int(input("Enter your choice (1-6): ")) - 1
        source_currency = currencies[source_choice]

        print("\nSelect target currency:")
        for i, currency in enumerate(currencies, start=1):
            print(f"{i}. {currency}")
        target_choice = int(input("Enter your choice (1-6): ")) - 1
        target_currency = currencies[target_choice]

        amount = float(input("Enter amount to convert: "))

        try:
            converted_amount = convert_currency(amount, source_currency, target_currency)
            print(f"{amount} {source_currency} = {converted_amount:.2f} {target_currency}")
        except requests.exceptions.RequestException as e:
            print("Error fetching exchange rate:", e)
        except Exception as e:
            print("Error:", e)

        again = input("Convert again? (y/n): ")
        if again.lower() != 'y':
            break

if __name__ == "__main__":
    main()
