# Currency-converter
import requests
from forex_python.converter import CurrencyRates

def get_user_input():
    amount= float(input("Enter the amount to be converted: "))
    source_currency= input("Enter the source currency (3-letter code, e.g., USD): ").upper()
    target_currency= input("Enter the target currency (3-letter code, e.g., EUR or INR): ").upper()
    return amount, source_currency, target_currency

def get_exchange_rate(source_currency, target_currency): 
    currency_rates = CurrencyRates()

    try:
        exchange_rate = currency_rates.get_rate(source_currency, target_currency) 
        return exchange_rate
    except Exception as e:
        print(f"Error fetching currency rates: {e}")
        return None

def convert_currency(amount, exchange_rate): 
    converted_amount = amount * exchange_rate 
    return converted_amount

def main():
    amount, source_currency, target_currency= get_user_input() 
    exchange_rate= get_exchange_rate(source_currency, target_currency)

    if exchange_rate is not None:
        converted_amount= convert_currency (amount, exchange_rate) 
        print(f"{amount} {source_currency} is equal to {converted_amount:.2f} {target_currency}")

if __name__=="__main__":
    main()
