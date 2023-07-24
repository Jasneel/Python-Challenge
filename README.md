# Python-Challenge
Code for PyBank ->


import os
import csv
filepath = os.path.join('.', 'Resources', 'budget_data.csv')

# Creating list to store data 
budget_data = []

# Opening the CSV
with open(filepath) as csvfile:
    reader = csv.DictReader(csvfile)

    # Looping through the data to store in a dictionary
    for row in reader:
        budget_data.append({"month": row["Date"], "amount": int(row["Profit/Losses"]),"change": 0})

# Calculating the total months
total_months = len(budget_data)

# Looping through the dictionary in order to calculate changes between months
previous_amount = budget_data[0]["amount"]
for i in range(total_months):
    budget_data[i]["change"] = budget_data[i]["amount"] - previous_amount
    prev_amount = budget_data[i]["amount"]

# Calculating the total amount
total_amount = sum(row['amount'] for row in budget_data) 

# Calculating the average of amount changes
total_change = sum(row['change'] for row in budget_data)
average = round(total_change / (total_months-1), 2)



# Printting the Final Analysis
print('Financial Analysis')
print('----------------------------')
print(f'Total Months: {total_months}')
print(f'Total: ${total_amount}')
print(f'Average Change: ${average}')



# Printting  the Final analysis and exporting to a text file 
# Set path for file
filepath = os.path.join("Analysis", "PyBank_Analysis.txt")
with open(filepath, "w") as text_file:
    print('Financial Analysis', file=text_file)
    print('----------------------------', file=text_file)
    print(f'Total Months: {total_months}', file=text_file)
    print(f'Total: ${total_amount}', file=text_file)
    print(f'Average Change: ${average}', file=text_file)
    

    # not sure how to calculate greatest increase/decrease in Profits












    Code for PyPoll ->

    
import os
import csv

filepath = os.path.join('.', 'Resources', 'election_data.csv')


with open(filepath, newline='') as csvfile:

    # CSV reader specifiing the delimiter and variable that holds contents within the file
    csvreader = csv.reader(csvfile, delimiter=',')

    # Reading the first row (header)
    csv_header = next(csvreader)

    candidate_list = [candidate[2] for candidate in csvreader]
    
# Calculating the number of total votes
total_votes = len(candidate_list)

# Creating a unique list of the candidates with the corresponding number of votes
canditates_info = [[candidate,candidate_list.count(candidate)] for candidate in set(candidate_list)]

# Sorting the list so that the first candidate becomes the winner 
canditates_info = sorted(canditates_info, key=lambda x: x[1], reverse=True)

# Printing the election results
print("Election Results")
print("-------------------------")
print(f"Total Votes: {total_votes}")
print("-------------------------")

for candidate in canditates_info:
    percent_votes = (candidate[1] / total_votes) * 100
    print(f'{candidate[0]}: {percent_votes:6.3f}% ({candidate[1]})')

print("-------------------------")
print(f"Winner: {canditates_info[0][0]}")
print("-------------------------")

 
# Set path for election results file
filepath = os.path.join('.', 'Analysis', 'PyPoll_Analysis.txt')
with open(filepath, "w") as text_file:
    print("Election Results", file=text_file)
    print("-------------------------", file=text_file)
    print(f"Total Votes: {total_votes}", file=text_file)
    print("-------------------------", file=text_file)

    for candidate in canditates_info:
        percent_votes = (candidate[1] / total_votes) * 100
        print(f'{candidate[0]}: {percent_votes:6.3f}% ({candidate[1]})', file=text_file)

    print("-------------------------", file=text_file)
    print(f"Winner: {canditates_info[0][0]}", file=text_file)
    print("-------------------------", file=text_file)
