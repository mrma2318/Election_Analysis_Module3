# Election_Analysis

## Project Overview
A Colorado Board of Elections employee has given me the following tasks to complete the election audit of a recent local congressional election. 

The purpose of this election audit is to report the total number of votes casts, total number of votes per candidate, percentage of votes per candidate, and the winner of the election based on popular vote.

## Resources
- Data Source: election_results.csv
- Software: Python 3.7.6, Visual Studio Code, 1.71.0

## Analysis and Challenges
### Analysis of Outcomes Based on Candidate
1. Calculate the total number of votes cast. 
    - Before I could caluclate the total number of votes cast, I needed to initalize a total vote counter. 
    - Code:

    total_votes = 0

2. Get a complete list of candidates who received votes. 
    - Once I opened the file I needed to load as election data, I needed to create a for loop that would add to the total vote count and get the candidates name from each row. However, I wanted to make sure that it was only collecting the candidates names once, and then adding to the total count when it appeared again. Therefore, I had to create and if statement inside my for loop. This allowed me to add the candidates name to the list if it wasn't there already, and then start tracking that candidate's vote count.
    - Code: 

    with open(file_to_load) as election_data:
    
        reader = csv.reader(election_data)
    
        header = next(reader)
    
        for row in reader:
    
            total_votes = total_votes + 1
    
            candidate_name = row[2]
    
            if candidate_name not in candidate_options:
    
            candidate_options.append(candidate_name)
    
            candidate_votes[candidate_name] = 0
    
        candidate_votes[candidate_name] += 1
        
3. Calculate the total number of votes each candidate received. 
    - After I completed the code for getting a list of candidates who received votes, and how many votes each candidate had, I needed to print the total number of votes for each candidate. 
    - Code: 
    election_results = (
        f"\nElection Results\n"
        f"-------------------------\n"
        f"Total Votes: {total_votes:,}\n"
        f"-------------------------\n\n"
        f"County Votes:\n")
    print(election_results, end="")
    txt_file.write(election_results)

4. Calculate the percentage of votes each candidate won. 
    - To get the total percent of votes each candidate won, I needed to divide the candidate's vote count by the total vote count, then multiple by 100. 
    - Code: 
    for candidate_name in candidate_votes:
        votes = candidate_votes.get[candidate_name]
        vote_percentage = float(votes) / float(total_votes) * 100
        print(f"{candidate_name}: received {vote_percentage:.1f}% of the vote.")

5. Determine the winner of the election based on popular vote. 
    - Lastly, to determine the winning candidate, vote count, and percentage, I needed to use a decision statement to compare the number of votes each candidate recieved. 
    - To do this, I first needed to declare three variables: winning candidate, winning count, and winning percentage. 
    - Code: 
    winning_candidate = ""
    winning_count = 0
    winning_percentage = 0
    - Next, I needed to create an if statement inside the for loop to determine if the vote count was greater than the winning count, and the percentage is greater than the winning percentage. 
    - Code: 
    if (votes > winning_count) and (vote_percentage > winning_percentage):
         winning_count = votes
         winning_percentage = vote_percentage
         winning_candidate = candidate_name
    print(f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n")
    - Finally, I needed to print out the winning candidate summary.
    - Code: 
    winning_candidate_summary = (
        f"-------------------------\n"
        f"Winner: {winning_candidate}\n"
        f"Winning Vote Count: {winning_count:,}\n"
        f"Winning Percentage: {winning_percentage:.1f}%\n"
        f"-------------------------\n")
    print(winning_candidate_summary)

### Analysis of Outcomes Based on County
In addition election audit to report the total number of votes casts, total number of votes per candidate, percentage of votes per candidate, and the winner of the election based on popular vote, the election commission requested additional data. The election commission wanted me to also audit the voter turnout for each county, the percentage of votes from each county, and determine which county had the highest turout. To complete this audit for the election commission, I completed the following flow chart.
1. Create a county list and county votes dictionary. 
    - Code: 
    county_list = []
    county_votes = {}

2. Track the largest county and county voter turnout. 
    - Code: 
    largest_county = ""
    county_turnout = 0
    turnout_percent = 0

3. Extract the county name from each row.
    - To complete this task, I needed to include the below code within the for loop I created previously for the candidate. 
    - Code: 
     county_name = row [1]

4. Check to see if the county name is in the county list. 
    - Code: 
        if county_name not in county_list:
            county_list.append(county_name)
            county_votes[county_name] = 0

5. Calculate the county's vote count.
    - Code: 
        county_votes[county_name] += 1

6. Calculate the percentage of votes for the county.
    - Code: 
    for county_name in county_votes:
        count = county_votes[county_name]
        count_percent = float(count)/float(total_votes) * 100
        county_results = (f"{county_name}: {count_percent: .1f}% ({count:,})\n")
        print(county_results)
        txt_file.write(county_results)

        if (count > county_turnout) and (count_percent > turnout_percent):
            county_turnout = count
            turnout_percent = count_percent
            largest_county = county_name
    winning_county_summary = (
        f"\n-------------------------\n"
        f"Largest County Turnout: {largest_county}\n"
        f"-------------------------\n")

7. Print the county with the largest turnout to the terminal. 
    - Code: 
     print(winning_county_summary)

Please referr to [PyPoll_Challenge.py](https://github.com/mrma2318/Election_Analysis_Module3/blob/aaca41ab6e4353fe2bcc0318a112793201f6d6de/PyPoll_Challenge.py) for completed and combined code analysis of the election data for both the candidate and county. 

Once the script had been completed and the analysis was successful, I printed the election results to it's own text file, [election_analysis.txt](https://github.com/mrma2318/Election_Analysis_Module3/blob/aaca41ab6e4353fe2bcc0318a112793201f6d6de/analysis/election_analysis.txt).

## Analysis Summary
The analysis of the election show that: 
- There were 369,711 votes cast in the election. 
- The number of votes and percentage of total votes for each county were: 
    - Jefferson county recieved 10.5% of the vote and 38,855 number of votes. 
    - Denver county received 82.2% of the vote and 306,055 numbr of the votes. 
    - Arapahoe county received 6.7% of the vote and 24,801 number of the votes. 
- The county with the largest number of votes was:
    - Denver county, who recieved 82.2% of the vote and 306,055 number of votes. 
- The candidates were: 
    - Charles Casper Stockham
    - Diana DeGette
    - Raymon Anthony Doane
- The candidate results were: 
    - Charles Casper Stockham recieved 23.0% of the vote and 85,213 number of votes.
    - Diana DeGette recieved 73.8% of the vote and 272,892 number of votes.
    - Raymon Anthony Doane recieved 3.1% of the vote and 11,606 number of votes.
- The winner of the election was: 
    - Diana DeGette, who recieved 73.8% of the vote and 272,892 number of votes. 
  
  ### Challenges and Difficulties


  ## Challenge Overview
  
  ## Challenge Summary
