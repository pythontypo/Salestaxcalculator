# Salestaxcalculator

"""This program is designed to help a cashier to calculate the sales tax and total price of a product.
This program also calculates the change if a customer paid with cash.
The program gives the exact number of bills and coins of each denomination.
The program excludes $2.00 bill, $1.00 coin, and $0.50 coin since these are rare.
python change.py
"""

CITY_TAX_RATE = 9.5 #Los Angeles sales tax in 2021 is 9.5%
CITY = "Los Angeles" #Change as needed


def main():
#the main function executes all other functions step by step
    print_intro() #prints the desctription of the program
    price = get_price() #user gives a product price, program checks if the entry is valid.
    tax = calculate_tax(price) #this function calculates the tax based on the price provided by the user.
    total_price = money_owed(tax,price) #this function calculates the total price including the tax.
    print_calculation(tax,price,total_price) #prints information about the tax rate in the city and calculated tax and total price
    money = money_received(total_price)  #user enters the amount of money received from the customer. The function checks if the entry is valid. 
    change = change_owed(money,total_price) #This function calculates the change owed to the customer
    bills(change,total_price) #this function gives the user the exact number of bills to give to the customer
    coins(change,total_price) #this function gives the user the exact number of coins to give to the customer
    

def print_intro():#prints the desctription of the program
    print("This program calculates a sales tax, a total price, and a change.")
    
    
def print_calculation(tax,price,total_price): #prints information about the tax rate in the city and calculated tax and total price
    print("The sales tax in " + CITY + " is " + str(CITY_TAX_RATE) + "%.")
    print("Based on the price you provided, the calculated sales tax is $" + "%1.2f" % tax + ".")
    print("The total price is $" + "%1.2f" % total_price + ".")
   

def get_price(): #user gives a product price, program checks if the entry is valid.
    while True:
        try:
            price = float(input("Enter the price before tax: $"))
        except ValueError:
            print('Invalid entry. Price should be entered in the following format: $0.00')
            continue
        else:
            break
    price = round(price,2)
    return price


def calculate_tax(price): #this function calculates the tax based on the price provided by the user.
    tax = (price * CITY_TAX_RATE) / 100
    tax = round(tax,2)
    return tax

def money_owed(tax,price): #this function calculates the total price including the tax.
    total_price = tax + price
    return total_price


def money_received(total_price): #user enters the amount of money received from the customer. The function checks if the entry is valid. 
    while True:
        try:
            money = float(input("Enter the amount of money received from the customer: $"))
        except: 
            print('Invalid entry. Please use the following format: $0.00')
            continue
        else:
            break
    while money < total_price:
        print("The customer gave you $" + "%1.2f" % money + " which is less than the total price of $" + "%1.2f" % total_price)
        while True:
            try:
                money = float(input("Enter the amount of money received from the customer: $"))
            except: 
                print('Invalid entry. Please use the following format: $0.00')
                continue
            else:
                break
    money = round(money,2)
    return money


def change_owed(money,total_price): #This function calculates the change owed to the customer
    change = money - total_price
    if money == total_price:
        print("The customer gave you the exact amount. No change is needed")
    else:
        print("The change is: $" +"%1.2f" % change)
    return change


def bills(change,total_price): #this function gives the user the exact number of bills to give to the customer
    if change != total_price:
        bill100 = int(change // 100)
        if bill100 >= 1:
            change = change - (bill100 * 100)
            print("Give the customer " + str(bill100) + " $100.00 bill(s).")
        bill50 = int(change // 50)
        if bill50 >= 1:
            change = change - (bill50 * 50)
            print("Give the customer " + str(bill50) + " $50.00 bill(s).")
        bill20 = int(change // 20)
        if bill20 >= 1:
            change = change - (bill20 * 20)
            print("Give the customer " + str(bill20) + " $20.00 bill(s).")
        bill10 = int(change // 10)
        if bill10 >= 1:
            change = change - (bill10 * 10)
            print("Give the customer " + str(bill10) + " $10.00 bill(s).")
        bill5 = int(change // 5)
        if bill5 >= 1:
            change = change - (bill5 * 5)
            print("Give the customer " + str(bill5) + " $5.00 bill(s).")
        bill1 = int(change // 1)
        if bill1 >= 1:
            change = change - bill1
            print("Give the customer " + str(bill1) + " $1.00 bill(s).")


def coins(change,total_price): #this function gives the user the exact number of coins to give to the customer
    if change != total_price:
        change = change - int(change)
        coin25 = change / 0.25
        if coin25  >= 1:
            change = change - (int(coin25) * 0.25)
            print("Give the customer " + str(int(coin25)) + " $0.25 coin(s).")
        coin10 = change / 0.10
        if coin10  >= 1:
            change = change - (int(coin10) * 0.10)
            print("Give the customer " + str(int(coin10)) + " $0.10 coin(s).")
        coin5 = change / 0.05
        if coin5  >= 1:
            change = change - (int(coin5) * 0.05)
            print("Give the customer " + str(int(coin5)) + " $0.05 coin(s).")
        coin1 = change / 0.01
        if coin1  >= 1:
            change = change - int(coin1)
            print("Give the customer " + str(int(coin1)) + " $0.01 coin(s).")

if __name__ == "__main__":
    main()




