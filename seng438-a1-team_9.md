>   **SENG 438 - Software Testing, Reliability, and Quality**

**Lab. Report \#1 – Introduction to Testing and Defect Tracking**

| Group: 9      |
|-----------------|
| Student 1 Zhifan Li        |   
| Student 2 Sandip Mishra              |   
| Student 3 Shanzi Ye             |   
| Student 4 Fardin Aryan                |   


**Table of Contents**

(When you finish writing, update the following list using right click, then
“Update Field”)

[1 Introduction	1](#_Toc439194677)

[2 High-level description of the exploratory testing plan	1](#_Toc439194678)

[3 Comparison of exploratory and manual functional testing	1](#_Toc439194679)

[4 Notes and discussion of the peer reviews of defect reports	1](#_Toc439194680)

[5 How the pair testing was managed and team work/effort was
divided	1](#_Toc439194681)

[6 Difficulties encountered, challenges overcome, and lessons
learned	1](#_Toc439194682)

[7 Comments/feedback on the lab and lab document itself	1](#_Toc439194683)

[SENG438 A1 Jira Issues as Excel Sheet](https://github.com/seng438-winter-2024/seng438-a1-zhifanl/blob/main/seng438-a1-jira-issues.csv "View the SENG438 A1 Jira Issues CSV")


# Introduction

In this laboratory work, we delve into the realm of software testing, focusing on an ATM machine simulation system. Prior to this lab, my experience with software testing was primarily limited to unit testing, which involved checking individual code functions, often neglecting comprehensive end-to-end testing. The lab aims to expand this knowledge through the application of exploratory, manual scripted, and regression testing methods. Exploratory testing offers a flexible, intuitive approach, while manual scripted testing provides a structured, scenario-based framework. Regression testing ensures that new changes don't disrupt existing functionalities. This multi-faceted approach promises a thorough evaluation of the ATM system, contributing significantly to my understanding of diverse and effective software testing practices.

# High-level description of the exploratory testing plan

high-level exploratory test plan:

## Zhifan & Shanzi: (Testing Pair #1):

For executing the testing plan:

We are planning to test most of the features including the edge cases. For the purpose of exploratory testing, we will try to keep these tests as random as possible. 
We will begin by testing by using the two accounts provided in the README file.

1.We want to make sure the power can start up and shut down normally when operators perform it. and also make sure the card can be inserted normally and ejected normally no matter if the transaction is successful or any failure happens.

2.we want to make sure the account id, pin number are correct and only the correct data can enter the system. We will throw some random inputs to test if these will be validated by the system or not. The incorrect account or pin numbers will cause the system to deny the access, after three times of successfully attempting to login, the system will lock the card permanently and the user has to contact the bank to get it unlocked.

3.We want to make sure monetary transfers such as deposits and withdrawals work normally by entering a variety of random values including edge cases to both chequing, saving, and money market. (For example, we will try entering 20, 40, 60, 2000)We will check the balances to see if the result matches with the expected outcome, including canceling the transaction during the stage of the process. If any bug happens, we will record and try to find the root cause, see if it is a common bug for all deposits or withdrawals and we also plan to record the state and steps we performed for us to easily reproduce the bug. 

4.We want to make sure the system can do monetary transfers such as transferring to linked accounts and making an inquiry. 

5.During each type of transaction, we will click cancel to ensure this feature correctly cancels the operation. We will be clicking cancel at different times during the transaction to make sure that a user is able to abort at any given moment.

6.We then want to make sure the logging feature acts normally, all the actions are recorded and there are no missing records of actions. 

7.We also want to test if the system is giving the correct textual prompt to the user, to make sure the UI doesn’t give any ambiguity such as incorrect words or numbers. 

Defects:

1.No error message when entering the wrong card number, if a customer enters the wrong card number accidentally, then the PIN will keep getting wrong, which results in the customer’s card getting locked.
2.previous log & output not getting cleared when shutdown or restarting the ATM machine
3.when transferring money >0.5 between linked accounts, 0,5$ is taken from the bank
4.when transferring money <0.5 between linked accounts, the money transferred becomes a negative number, which causes the target account to actually lose money.
5.UI error: “Wood” you like another translation
6.Cannot transfer from money market to chequing or saving
7.Cannot transfer from chequing or saving to money market
8.Cannot make inquiry for Saving account, no such option
9.Cannot make inquiry about the money market. When selecting money market, it shows the saving account’s balance
10.when depositing 10000000.00 dollars, the system crashes. Cannot even insert an envelope.

Test#1: (Card 1)
Login in first card with #1, Password 42
Expected Result: Successful Login
Actual: Successful Login
Status: Pass
Regression Testing: Pass

Test#2: (Card 1)
Show balance inquiry for checking account
Expected Result: $100
Actual: $100
Status: Pass
Regression Testing: Pass

Test#3: (Card 1)
Transfer 20$ from chequing to saving
Expected Result: $1020 in saving
Actual: $1019.5
Status: Fail
Regression Result: $1020
Regression Testing: Pass

Test#4: (Card 1)
Transfer 0.4$ from chequing to saving
Expected Result: $1000.4 in saving
Actual: $999.9
Status: Fail
Regression Result: $1000.4
Regression Testing: Pass

Test #5 : (Card 1)
Check Balance inquiry page
Expected Result: Show checking + Savings + Money Market options
Actual: Shows Checking + Money Market options
Status: Fail
Regression Result: Show checking + Savings + Money Market options
Regression Stat   : Pass

Test #6 : (Card 1)
Transfer $20 from Chequing to money market
Expected Result: $20 into money market
Actual: Invalid to account type
Status: Fail
Regression Result:  Invalid to account type
Regression Stat: Fail

Test #7 : (Card 1)
Transfer $20 from Saving to money market
Expected Result: $20 into money market
Actual: Invalid to account type
Status: Fail
Regression Result:  Invalid to account type
Regression Stat   : Fail

Test #8 : (Card 1)
Deposit $2000 to chequing
Expected Result: $2100
Actual: TOTAL BAL: $2090.00, AVAILABLE: $100.00
Status: Fail
Regression Result: TOTAL BAL: $2099.90, AVAILABLE: $100.00
Regression Stat   : Fail

Test #9 : (Card 1)
Deposit $2000 to saving
Expected Result: $3000
Actual:TOTAL BAL: $2990.00, AVAILABLE: $1000.00
Status: Fail
Regression Result:TOTAL BAL: $2099.90, AVAILABLE: $100.00
Regression Stat   : Fail

Test #10 : (Card 1)
Deposit $100000 to saving
Expected Result: $103000
Actual:TOTAL BAL: $102990.00, AVAILABLE: $1000.00
Status: Fail
Regression Result:TOTAL BAL: $102990.00, AVAILABLE: $1000.00
Regression Stat   : Fail

Test #11 : (Card 1)
Balance Inquiry of Money Market
Expected Result: Money Market’s balance
Actual: Unknown error first, then cannot make inquiry for money market. When selecting money market, it shows the saving account’s balance
Status: Fail
Regression Result: Invalid Account Type
Regression Stat   : Fail

Test #12 : (Card 1)
Deposit 100000000 to chequing
Expected Result: Chequing gets updated, or show error message
Actual: No error message shown, no update
Status: Fail
Regression Result: Same
Regression Stat   : Fail


## Sandip Mishra & Fardin Aryan: (Testing Pair #2):

Our main approach to this exploratory testing phase consists of breaking this program down into its innate functionalities. These include:

### Withdrawing
#### Checking
- Amount of Cash (20-200)
  - Show Selected Amount
  - Show Receipt
  - Prompt Transaction

#### Savings (No saving Account for Card 2)
- Amount of Cash (20-200)
  - Show Selected Amount
  - Show Receipt
  - Prompt Transaction

#### Money Market (No Money market for card 1)
- Amount of Cash (20-200)
  - Show Selected Amount
  - Show Receipt
  - Prompt Transaction

 ### Depositing
#### Checking
- Amount of Cash (20-200)
  - Envelope
  - Show Receipt
  - Prompt Transaction

#### Savings
- Amount of Cash (20-200)
  - Envelope
  - Show Receipt
  - Prompt Transaction

#### Money Market
- Amount of Cash (20-200)
  - Envelope
  - Show Receipt
  - Prompt Transaction

### Login
- Inserting Card
  - Enter card number
    - Pin
    - Prompt transaction type

### Transfer
- Select Account from
  - Select Account to
    - Select Amount (any)
    - Show Receipt
    - Prompt Transaction

### Balance
- Select Account
  - Show Receipt
  - Prompt Transaction


Test#1: (Card 2)
Login in card with #1, Password 1234
Expected Result: Successful Login
Actual: Successful Login
Status: Pass
Regression Testing: Pass


Test\#2: (Card 2) Show balance inquiry for checking account Expected Result: \$100 Actual: \$100 Status: Pass Regression Testing: Pass

Test\#3: (Card 2) Transfer \$20 from Checking to Money Market Expected Result: \$5020 in Money Market Actual: \$5019.5 Status: Fail Regression Result: \$5020 Regression Testing: Pass



Test#4: (Card 2)
Transfer 0.88$ from Money Market to Checking
Expected Result: 81.76 $ transferred 
Actual: $ 81.26
Status: Fail
Regression Result: 81.76$
Regression Testing: Pass


Test #5 : (Card 2)
Balance Inquiry of Money Market account
Expected Result: Shows current balance of Money Market account
Actual: Outputs “Invalid Account type”
Status: Fail
Regression Result: Shows current balance of Money Market account
Regression Stat   : Pass
Test #6 : (Card 2)
Transfer $20 from money market to checking
Expected Result: Transfer occurs from money market to checking 
Actual: Receipt prints that Transfer occurs from checking to money market 
Status: Fail
Regression Result:  Receipt prints that Transfer occurs from checking to money market
Regression Stat: Fail


Test #7 : (Card 2)
Withdraw $40 from checking
Expected Result: $60 remaining on checking
Actual: $40 remaining on checking
Status: Fail
Regression Result:  $60 remaining on checking
Regression Stat   : Pass


Test #8 : (Card 2)
Withdraw $100 from Money Market
Expected Result: Total Balance- $4900
Actual: “Invalid Account type”
Status: Fail
Regression Result: Total Balance-$4900
Regression Stat   : Pass
Test #9 : (Card 2)
Deposit $800 to Money Market
Expected Result: Total Balance- $5800
Actual:Total Balance- $5790
Status: Fail
Regression Result:Total Balance- $5799.90
Regression Stat   : Fail


Test #10 : (Card 2)
Deposit $350 to Checking
Expected Result: Total balance- $ 450
Actual: Total balance- $440
Status: Fail
Regression Result:Total balance- $449.90
Regression Stat   : Fail




# Comparison of exploratory and manual functional testing

Exploratory and manual functional testing are two completely different testing methods. Manual functional testing can’t be started until a detailed testing plan is made, hence it requires testers to prepare a manual scripted testing plan that contains all the basic functionalities the system needs to meet. Exploratory testing is a more flexible testing method that allows testers to test the system over a broader range. Exploratory testing emphasizes the defects and issues that consumers might encounter in the real world and the testers toi freely explore the system and find the bugs that are not listed in the manual scripted test cases.

Compared to the manual functional testing, exploratory testing allows the programmer to have more freedom to test the system and go beyond the predefined testing cases. In this lab, we found some bugs exist in the system that are not listed in the manual test cases by using exploratory testing. However, we felt that exploratory testing is a bit disorganized because normally we don’t follow a specific logic to test the system. When it comes to a large and complicated system, it’s difficult to cover every aspect thoroughly and conduct comprehensive testing. In contrast, manual functional testing is more efficient and organized. Since all the test cases have been clearly provided, we just need to split the task and test the system based on the testing cases. We have a clear objective and direction where we aim to test.


# Notes and discussion of the peer reviews of defect reports

During the exploratory testing stage, both teams came up with a detailed testing plan: Comprehensive coverage of functionalities, validation testing of ATM, and partitioned test cases including extreme edge cases. 

Comprehensive Coverage: The plan included a wide range of tests covering key ATM functionalities such as start-up/shutdown processes, card handling, and transaction processing.
Security and Validation Testing: Testing for account access security, specifically the response to incorrect PIN and account inputs, was well-addressed.
Diverse Transaction Testing: The inclusion of various transaction types (deposits, withdrawals, transfers) across different account types is commendable.

Areas for Improvement:
Error Analysis: While errors were identified, a deeper analysis of the root causes would be beneficial for targeted fixes.

During these tests, various defects were identified. These included the absence of an error message when entering a wrong card number, issues with log and output not clearing upon system restart, problems with specific transaction types, and incorrect UI prompts. Notably, issues were found in transferring money between linked accounts, with incorrect deductions or additions of funds, and UI errors like "Wood you like another translation" instead of "Would you like another transaction." 
The test results showed a mix of passes and failures, highlighting areas where the system performed as expected and areas needing improvement. For example, balance inquiries for checking accounts passed, while transfers between certain account types and large deposit handling failed.


# How the pair testing was managed and team work/effort was divided 

Here’s how we conducted pair testing:

Testing Pair #1: Zhifan and Shanzi

Testing Pair #1 were responsible for manual scripted testing and regression testing. The assignment instructions listed 40 test cases, so we decided that each person would conduct 20 cases for both testing methods. Initially, we tested version 1.0, with Shanzi Ye handling cases 1 to 20 and Zhifan Li covering cases 21 to 40. Afterwards, we recorded our results in a Google doc. We then repeated this process for version 1.1. Finally, we compared the results to identify bugs in both versions.
For exploratory testing, Testing Pair #1 are primarily responsible for assisting Testing Pair #2 in identifying additional bugs that exist in both versions. A detailed high-level exploratory test plan can be found above.

Testing Pair #2: Sandip Mishra and Fardin Aryan

Testing Pair #2 was primarily responsible for exploratory testing. They conducted exploratory testing by breaking the program down into its core functionalities, which included, but were not limited to, withdrawal, deposit, and transfer. Each person tested a certain number of functionalities and recorded the results in Google Docs. A detailed high-level exploratory test plan can be found above.
Testing Pair #2 was also responsible for recording the bugs on JIRA and generating the final bug report.
For the lab report, we all contribute to writing and proofreading it. We split the work equally, with everyone contributing to the assignment. 


# Difficulties encountered, challenges overcome, and lessons learned

In the beginning, we found it quite challenging to understand the assignment requirements because seng438-a1.md is lengthy and tedious to read. Then we had a group discussion in the lab and went through every detail in the instruction, which helped us understand the objective and the requirements.
Another difficulty we encountered is the use of Jira. None of us used this software so initially we had no idea how to report the bugs and its details on Jira. However, we were able to overcome this difficulty because we read some tutorials on google and spent some time getting familiar with the software.
In addition, we thought it was challenging to find the time slot when everyone was available to attend the group meeting. To solve this issue, we all filled out a form on When2meet and finally found the best time for us to meet in person or on discord.
After finishing this assignment, we understand that communication and team collaboration play an essential role in group projects as it helps us overcome difficulties, share ideas, and finish the assignment more efficiently.

# Comments/feedback on the lab and lab document itself

We think this lab assignment is very helpful to give us a general understanding of the testing process as most of us have zero testing experience. After this lab, we know how software testing works and what the key components of testing methods are. We learned various testing methods such as exploratory testing, manual scripted testing, as well as the differences between them. This lab also enhances our critical thinking ability and teaches us how to apply testing methods to improve a software’s functionality. By working as a group, this lab also teaches us how to split the workload and discover the most efficient way for team collaboration.


Despite the fact that the lab document is a bit lengthy and hard to read, it provides detailed instructions for us to conduct the testing. It allows us to follow the testing procedures step by step and finish the assignment efficiently. Overall, we believe that this assignment builds a solid foundation for future learning in this course.

