# Fraud Dectection

### - Capstone Project - Final project

#### Introduction:
Every since with got introduce to online payment digital, our life change for the majority of people. It's revolutionary is mean that we can pay in our comfort of ours homes without making any move. However, all good things have both sides of the coin. People with bad intentions can take advantage of the system to make transactions that will benefit them in their pocket.
Fun Facts : A total of 14,202 extortion frauds were reported to the Canadian Anti-Fraud Center (CAFC) in 2021, an average of nearly 40 per day. In fact this is  why I decided to do a credit fraud dection project and if we can be able to dectect fraud on a given dataset.


### Context:

PaySim simulates mobile money transactions based on a sample of real transactions extracted from one month of financial logs from a mobile money service implemented in an African country. The original logs were provided by a multinational company, who is the provider of the mobile financial service which is currently running in more than 14 countries all around the world.

This synthetic dataset is scaled down 1/4 of the original dataset and it is created just for Kaggle.



## Goals:

The main  goals of this project is to be able to predict whenever the transacion is fraudulant or not by trying to build a machine learning model to classify fraud and non-fraud transactions.


## Dataset description

<br>1 -step - maps a unit of time in the real world. In this case 1 step is 1 hour of time. Total steps 744 (30 days simulation).
<br>2 -type - CASH-IN, CASH-OUT, DEBIT, PAYMENT and TRANSFER.
<br>3 -amount - amount of the transaction in local currency.
<br>4 -nameOrig - customer who started the transaction
<br>5 -oldbalanceOrg - initial balance before the transaction
<br>6 -newbalanceOrig - new balance after the transaction
<br>7 -nameDest - customer who is the recipient of the transaction
<br>8 -oldbalanceDest - initial balance recipient before the transaction. Note that there is not information for customers that start with M (Merchants).
<br>9 -newbalanceDest - new balance recipient after the transaction. Note that there is not information for customers that start with M (Merchants).
<br>10 -isFraud - This is the transactions made by the fraudulent agents inside the simulation. In this specific dataset the fraudulent behavior of the agents aims to profit by taking control or customers accounts and try to empty the funds by transferring to another account and then cashing out of the system.
<br>11 -isFlaggedFraud - The business model aims to control massive transfers from one account to another and flags illegal attempts. An illegal attempt in this dataset is an attempt to transfer more than 200.000 in a single transaction.


## EDA

#### Cleaing The Data :

1. There not much cleaning to do because the dataset have no duplicates or missing values. 


# Data visualisation

#### Before digging in building a machine learning, let's visualize some data. 



1. As we can, see the most popular type of transaction is cash_out and payment
<img src="image/Capture d’écran_20221205_054424.png" style="width: 480px"/> 



2. As we can see , we can compare the different type of transaction peoples were making(categorize by fraud or not)
<img src="image/Capture d’écran_20221205_054535.png" style="width: 720px"/>




3. Between the fraudlent transaction only two type of transaction seems  to be favored, the cash_out option and Transfer
<img src="image/Capture d’écran_20221205_054544.png" style="width: 400px"/>

There are four types of transaction in the dataset but only two were used to make suspicious payment. In the 8213 fraudlent transactions 4116 is cash_out and 4097 is transfer money


### Models and Metrics

Because the dataset were very unbalanced , Only 0,13 % of the entire dataset which correspond to 8213 have a fraudulent transaction compare to the regular one (without fraud) which is 6354407. We must definitely try to balance the data because otherwise the data can be confusing. Indeed, most of the time the percentage of precision is close to 100. It will badly predict the data which are rare because the model  is not used to seeing it.

1. I use three different methods to resample the data the best that I could to balance the dataset. After that , I used logistic regression
on all three of them to see which of is better for resample the unbalnce data.

2 .I also use metrics like  random forest classifier , XGBClassifier , SVC



## Results:

#### Random Forest Classifier

                   precision  recall  f1-score    support

             0.0       1.00      1.00      1.00    402823
             1.0       0.96      0.69      0.80       465

        accuracy                           1.00    403288
       macro avg       0.98      0.84      0.90    403288
    weighted avg       1.00      1.00      1.00    403288
    


#### Random Forest Classifier(SMOTE)

                   precision  recall    f1-score   support

             0.0       1.00      1.00      1.00   1079283
             1.0       0.97      0.73      0.83       913

        accuracy                           1.00   1080196
       macro avg       0.99      0.86      0.92   1080196
    weighted avg       1.00      1.00      1.00   1080196



#### Random Under Sampling  Logistic XGBClassifier() Regression SVC

                   precision  recall   f1-score    support

             0.0       0.91      0.92      0.92       667
             1.0       0.91      0.91      0.91       625

        accuracy                           0.91      1292
       macro avg       0.91      0.91      0.91      1292
    weighted avg       0.91      0.91      0.91      1292



Logistic XGBClassifier() :

Accuracy score is: 0.9775541795665634

ROCAUC score: 0.9777571214392804

F1 score: 0.976965845909452


Regression SVC:

ROCAUC score: 0.8913307346326836

Accuracy score: 0.8908668730650154

F1 score: 0.8892380204241949

#### Generate_synthetic_samples(SMOTE) Logistic Regression XGBClassifier()

                   precision  recall  f1-score  support

             0.0       1.00      0.93      0.96    251664
             1.0       0.01      0.96      0.01       140

        accuracy                           0.93    251804
       macro avg       0.50      0.94      0.49    251804
    weighted avg       1.00      0.93      0.96    251804

   
       
       
XGBClassifier(): 

Accuracy score is: 0.966557322361837

ROCAUC score: 0.9725610337592981

F1 score: 0.031512363427257044



# Conclusion :

If I have to choose the best model to predict the outcomes of a transaction , it will probably be under the model of logistic regression 
or Regression SVC with the data being split with random under sampling. In fact ,  between the four method that I used the random under sampling was the best of them four who was able unbalance better the  data before putiing in my model.(Random Forest Classifier(SMOTE) was the second best). 

Also , with the help with the confusion matrix , the model predict successfully predict 611 not fraud transaction and 568 fraud transaction(False transaction). However ,  the model predict wrongfully predict that 57 transaction going to be not fraudulent but were and  56  fraud transaction.

#### True positive : 611
#### True negative : 568
#### False positive : 57
#### False negative: 56


<img src="image/Capture d’écran_20221206_073354.png" style="width: 400px"/>
