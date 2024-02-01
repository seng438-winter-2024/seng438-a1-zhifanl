>   **SENG 438 - Software Testing, Reliability, and Quality**

**Lab. Report \#1 – Introduction to Testing and Defect Tracking**

| Group: Group Number      |
|-----------------|
| Student 1 Zhifan Li 30089428        |   
| Student 2 Sandip Mishra              |   
| Student 3 Shanzi Ye               |   
| Student 4 Fardin Aryan 3016150                |   


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

# Introduction

In this laboratory work, we delve into the realm of software testing, focusing on an ATM machine simulation system. Prior to this lab, my experience with software testing was primarily limited to unit testing, which involved checking individual code functions, often neglecting comprehensive end-to-end testing. The lab aims to expand this knowledge through the application of exploratory, manual scripted, and regression testing methods. Exploratory testing offers a flexible, intuitive approach, while manual scripted testing provides a structured, scenario-based framework. Regression testing ensures that new changes don't disrupt existing functionalities. This multi-faceted approach promises a thorough evaluation of the ATM system, contributing significantly to my understanding of diverse and effective software testing practices.

# High-level description of the exploratory testing plan

high-level exploratory test plan:
Testing Pair #1: Zhifan and Shanzi
For executing the testing plan:
We are planning to test most of the features including the edge cases. For the purpose of exploratory testing, we will try to keep these tests as random as possible. 
We will begin by testing by using the two accounts provided in the README file.
we want to make sure the power can start up and shut down normally when operators perform it. and also make sure the card can be inserted normally and ejected normally no matter the transcrtion is successfully or any failure happens.
we want to make sure the account id, pin number are correct and only the correct data can enter the system. We will throw some random inputs to test if these will be validated by the system or not. The incorrect account or pin numbers will cause system to deny the access, after three times of uncessfully attempt to login, the system will lock the card permanently and the user has to contact bank to get it unlocked.
we want to make sure monetary transfer such as deposits and withdrawals work normally by entering a variety of random values including edge cases to both chequing, saving, and money market. (For example, we will try entering 20, 40, 60, 2000)We will check the balances to see if the result matches with the expected outcome, including canceling the transaction during stage of process. If any bug happens, we will record and try to find root cause, see if it is a common bug for all deposits or withdrawals and we also plan to record the state and steps we performed for us to easily reproduce the bug. 
we want to make sure the system can do monetary transfer such as transferring to linked account and make an inquiry. 
During each type of transaction, we will click cancel to ensure this feature correctly cancels the operation. We will be clicking cancel at different times during the transaction to make sure that a user is able to abort at any given moment.
We then want to make sure the logging feature acts normally, all the actions are recorded and there is no missing records of actions. 
We also want to test if the system is giving the correct textual prompt to the user, make sure the UI doesn’t give any ambiguity such as incorrect words or numbers. 


# Comparison of exploratory and manual functional testing

## Defects found in exploratory testing

Shanzi & Zhifan:
Test#1: No error message when entering the wrong card number
Test#2: previous log & output not getting cleared when shutdown or restarting the ATM machine
Test#3: when transferring money >0.5 between linked accounts, 0,5$ is taken from the bank
Test#4: when transfer money <0.5 between linked accounts, the money transferred becomes a negative number, which causes the target account to actually lose money.
Test#5: UI error: “Wood” you like another translation
Test#6: Cannot transfer from money market to chequing or saving
Test#7: Cannot transfer from chequing or saving to money market
Test#8: Cannot make inquiry for Saving account, no such option
Test#9: Cannot make inquiry for money market. When selecting money market, it shows the saving account’s balance
Test#10: when depositing 10000000.00 dollars, the system crashes. Cannot even insert an envelope.

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
Transfer 20$ from cheqing to saving
Expected Result: $1020 in saving
Actual: $1019.5
Status: Fail
Regression Result: $1020
Regression Testing: Pass

Test#4: (Card 1)
Transfer 0.4$ from cheqing to saving
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
Expected Result: Money Market’s blance
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

## Defects found in Manual Scripted testing:

-   Note that you need to submit a report generated by your defect tracking
    system, containing all defects recorded in the system.

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

Text…

# Difficulties encountered, challenges overcome, and lessons learned

Text…

# Comments/feedback on the lab and lab document itself

Text…
