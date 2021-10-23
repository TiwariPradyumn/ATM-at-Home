# ATM-at-Home
This function allow users to access their account balance, change pin, transact money from any place.
import pandas as pd
data=pd.read_csv("C:\\Users\\p8928\\Documents\\account.csv")
print(data)
list_pin=[]
list_adhar=[]
list_amount=[]
for i in range(5):
    list_pin.append(data.loc[i].at["Pin"])   
    list_adhar.append(data.loc[i].at["Aadhar"]) 
    list_amount.append(data.loc[i].at["Amount"]) 

class debit_card:

    def __init__(self):
        pass

    def verify_pin(self,pin):
        print("verifying pin...")
        if pin in list_pin:
            pin_loc=list_pin.index(pin)
            print("pin verified")
            adhar=int(input("Enter last 4 digit of Aadhar "))
            print("verifying aadhar...")
            if adhar==list_adhar[pin_loc]:
                print("Aadhar number verified")
                print("Connecting to server...")
                print("Your transaction is in process.")
                
            else:
                print("Aadhar number not verified")
                print("wrong input")
        else:
            print("pin not verified")
            print("try again (-_-)")
Pin=int(input("Enter Pin ")) 
obj=debit_card()
obj.verify_pin(Pin) 
print("Press 1 For Cash Withdraw \n","Press 2 To Check Balance \n","Press 3 To Change Pin")
inp=int(input())
if inp==1:
    Amount=int(input("Enter Amount Of Transaction "))
    pin_loc=list_pin.index(Pin)
    data.loc[pin_loc,"Amount"]=list_amount[pin_loc]-Amount
    data.to_csv("C:\\Users\\p8928\\Documents\\account.csv" , index=False)
    print("Remaining Account Balance is ",data.loc[pin_loc,"Amount"])
    print(data)  
elif inp==3:
    pin_loc=list_pin.index(Pin)
    new_pin=int(input("Enter new pin "))
    conf_pin=int(input("Confirm new pin "))
    if new_pin==conf_pin:
        data.loc[pin_loc, 'Pin'] = new_pin
        data.to_csv("C:\\Users\\p8928\\Documents\\account.csv" , index=False)
        print("Pin Number Successfully Changed")
        print(data)
    else:
        print("New pin and confirm new pin didn't matched") 
elif inp==2:
    pin_loc=list_pin.index(Pin)
    print("Your Account Balance is ",list_amount[pin_loc])
else:
    print("Thank You For Using Me")
