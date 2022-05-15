# python-challenge
##budget data

import pandas as pd

#open/view CSV file
csv_path = "/Users/daniellesears/Downloads/budget_data.csv"

df = pd.read_csv(csv_path)
df.head()

#Calculate the total number of months included in this dataset
Months = df["Date"].count()

#calculate net total profit/losses over entire period
sum = 0

for x, y in df.iterrows():
    sum+=(y["Profit/Losses"]) 

print (sum)

#Calculate the changes in "Profit/Losses" over the entire period, and then the average of those changes

Previous_Value=0
Sum_Change=0
Net_Change=[]

for x, y in df.iterrows():
    #print(x)
   # print(y)
    if x > 0:
        Difference = (y["Profit/Losses"])-Previous_Value
        Sum_Change = Difference + Sum_Change
    Net_Change.append(Difference)
    Previous_Value = (y["Profit/Losses"])
       
df["Sum_Change"]=Net_Change
df
   
#Calculate the greatest increase in profits
GreatestIncrease = df["Sum_Change"].max()
Gi_Date = df[df["Sum_Change"] == GreatestIncrease]["Date"]


# #Calculate the greatest decrease in profits
GreatestDecrease = df["Sum_Change"].min()
Gd_Date = df[df["Sum_Change"] == GreatestDecrease]["Date"]

#Print the financial analysis

print ("Financial Analysis")

print("Total Months:", Months)
print ("Total:", sum)
print("Average Change:", Sum_Change/85)
print(f"Greatest Increase in Profits: {Gi_Date}  ({GreatestIncrease})")
print(f"Greatest Decrease in Profits: {Gd_Date} ({GreatestDecrease})")
