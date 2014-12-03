pa8
===

wut am i doing?


# Author: Daniel Huval
# CLID:   dhh5741   
# Course/Section: CMPS 150 – Section 11
# Assignment: pa8
# Date Assigned: Sunday, November 23, 2014
# Date/Time Due: Tuesday, December 2, 2014 –- 11:55 pm
#
# Description: A program that handles types of transactions for different
# bank accounts.
#
# Certification of Authenticity:
# I certify that this assignment is entirely my own work.
class BankAccount:
    def __init__(self,account,inputamount):
        self.__account = account
        self.__balance = inputamount
        self.__numdeposits = 0
        self.__numwithdrawals = 0
        self.__totaldeposits = 0
        self.__totalwithdrawals = 0
    def getAccount(self):
        return self.__account
    def getBalance(self):
        return self.__balance
    def getNumDeposits(self):
        return self.__numdeposits
    def getNumWithdrawals(self):
        return self.__numwithdrawals
    def getTotalDeposits(self):
        return self.__totaldeposits
    def getTotalWithdrawals(self):
        return self.__totalwithdrawals
    def Deposit(self,amount):
        self.__balance = self.__balance + amount
        self.__numdeposits = self.__numdeposits + 1
        self.__totaldeposits = self.__totaldeposits + amount
    def Withdrawal(self,amount):
        if (self.__balance >= amount):
            self.__balance = self.__balance - amount
            self.__numwithdrawals = self.__numwithdrawals + 1
            self.__totalwithdrawals = self.__totalwithdrawals + amount
            return True
        else:
            return False
def main():
    file = input("Enter name of the file containing bank transactions:")
    infile=open(file,'r')
    account1 = infile.readline().strip()
    balance1 = eval(infile.readline())
    account2 = infile.readline().strip()
    balance2 = eval(infile.readline())
    account3 = infile.readline().strip()
    balance3 = eval(infile.readline())
    acc1 = BankAccount(account1,balance1)
    acc2 = BankAccount(account2,balance2)
    acc3 = BankAccount(account3,balance3)
    trans_type=infile.readline().strip()
    acc=infile.readline().strip()
    amount=eval(infile.readline()) 
    while trans_type != "#":       
        if trans_type=="D":
            if acc== account1:
                acc1.Deposit(amount)
                PrintSuccessfulTrans(account1,trans_type,acc1.getBalance())
            elif acc== account2:
                acc2.Deposit(amount)
                PrintSuccessfulTrans(account2,trans_type,acc2.getBalance())            
            elif acc== account3:
                acc3.Deposit(amount)
                PrintSuccessfulTrans(account3,trans_type,acc3.getBalance()) 
        if trans_type =="W":
            if acc == account1:
                status=acc1.Withdrawal(amount)
                if status == True:
                    PrintSuccessfulTrans(acc,trans_type,amount,acc1.getBalance())
                else:
                    PrintDenied(acc,trans_type,amount,"<denied>")
            elif acc == account2:
                status=acc2.Withdrawal(amount)
                if status == True:
                    PrintSuccessfulTrans(acc,trans_type,amount,acc2.getBalance())
                else:
                    PrintDenied(acc,trans_type,amount,"<denied>")
            elif acc == account3:
                status=acc3.Withdrawal(amount)
                if status == True:
                    PrintSuccessfulTrans(acc,trans_type,amount,acc3.getBalance())
                else:
                    PrintDenied(acc,trans_type,amount,"<denied>")
        if trans_type=="B":
            if acc == account1:
                PrintBalanceInquiry(acc,trans_type,acc1.getBalance())
            if acc == account2:
                PrintBalanceInquiry(acc,trans_type,acc2.getBalance())
            if acc == account3:
                PrintBalanceInquiry(acc,trans_type,acc3.getBalance())
        trans_type=infile.readline().strip()
        acc=infile.readline().strip()
        amount=eval(infile.readline())         
def PrintSuccessfulTrans(acc,type,amount,balance):
    # this is a function for printing a successful deposit/withdrawal
    acc=acc
    trans_type = ConvertType(type)
    print("{:1}{:12}{:8.2f}{:>12}".format(acc,trans_type,amount,balance))
def PrintDenied(account,trans_type,amount,msg):
    # this is a function for printing an denied withdrawal
    trans_type = ConvertType(type)
    print("{:1}{:12}{8.2f}{:>12}".format(acc,trans_type,amount,msg,))
def PrintBalanceInquiry(account,trans_type,balance):
    trans_type = ConvertType(type)
    print("{:1}{:12}{8.2f}".format(account,trans_type,balance))
def ConvertType(type):
    if (type == 'D'):
        return "Deposit"
    elif (type == 'W'):
        return "Withdrawal" 
    elif type == "T":
        return "Transfer"
    else:
        return "Balance Inquiry"

            
main()
