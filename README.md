 Affiliate Comparison
=======================
A check on data consistency across 2 data sources.

This repository contains all the code to reproduce the results and findings below.

A simple script written in python has been created to execute the comparison of the data sets downloaded from ShopBack affiliate networks and the data sets downloaded from the new commission tables in our database. 

Abstract 
--------

Currently, the data needed to generate the Daily Transaction Report (DTX) is manually downloaded from 18 different affiliate networks, queried from the Staff Live DB and sent to us by the merchant team. In order to improve our efficiency and productivity, we aim to automate the generation of the DTX by querying all the data from our databases. However, due to the huge discrepancies between the data downloaded from affiliate networks and our databases in the past, it is not advisable to use data solely from the databases. With the new commission database up and running, we aim to use it to automate our DTX but this will only be possible if the data in the new commission database matches the data downloaded from affiliate network. 

For this project, I will be comparing the order amount, commission amount and shopping trip ID (ST) from the data sets downloaded from affiliate networks with that from the data sets downloaded from affiliate networks.

Data Source
-----------
Data used in this project to reproduce the same result are from 22 July 2016 to 24 July 2016: 

  * Web data: data downloaded from ShopBack's affiliate networks (DTX_final_combined.csv)
  * DB data : data queried from commission database 

Methodology 
-----------






Both data sets are first cleaned before being passed to the 2 different methods: Similarity Ratio and Match ST

### Cleaner

**Features:**
  * `currency_convert`: converts amounts in various currencies to SGD

    ``` 
    conversion_rate = {'USD': 1.36, 'AUD': 1.05, 'SGD': 1, 'MYR': 0.35, 'PHP': 0.029, 
    'CNY': 0.21, 'IDR': 0.0001,'INR': 0.02, 'GBP': 2.03, 'EUR': 1.62}
    
     ```

  * `clean_web_affiliate_name`: clean data in Web to match the data in DB
  * `clean_db_affiliate_name`: clean data in DB to match the data in Web

### Compare amount

This method will compare the order amount and commission amount in Web data with the order amount and commission amount in DB data to give us the similarity ratio, difference and error rate, grouped by the date.

#### Similarity ratio

This function gives us the ratio of similarity between the Web and DB's order amount and commission amount.

 ```
 if (DB order amount < Web order amount) : 
  100 * (DB order amount / Web order amount)
 else:
  100 * (Web order amount / DB order amount)
 ```
 
 ```
 if (DB commission amount < Web commission amount) :
  100 * (DB commission amount / Web commission amount)
 else:
  100 * (Web commission amount / DB commission amount)
 ```
 
#### Difference

This function gives us the difference between the Web and DB's order and commission amount.

* `DB order amount - Web order amount`

* `DB commission amount - Web commission amount `


#### Error Rate

This function gives us the error rate base on DB data.

* `100 * (( DB order amount - Web order amount) / DB order amount)`

* `100 * ((DB commission amount - Web commission amount) / DB commission amount)`

#### Sample Result

 ![image](https://cloud.githubusercontent.com/assets/19897222/17390538/905fed18-5a40-11e6-8f25-eff0ec337575.png)


### Match ST 

This method will:

* Check if ST is matched in Web, DB or both.
* Similarity ratio and difference in count of ST in Web and DB, grouped by affiliate networks.

  ```
  if Count of DB ST < Count of Web ST:
    Count of DB ST / Count of Web ST
  else:
    Count of Web ST / Count of DB ST 
  ```
  
* Number of missing ST in Web data, grouped by affiliate networks.

  > Note: Missing ST for each order is indicated by '-1' in Web data. This usually occur when people are not signed in when they go onto a shopping trip and made a purchase. Thus, their ST are not tracked.
  

### Sample Result 
![image](https://cloud.githubusercontent.com/assets/19897222/17392274/d6a3d542-5a4e-11e6-9de7-cd9d408e4c3c.png)

ST from both data sets are merged into 1 table and matched agaisnt each other.

![image](https://cloud.githubusercontent.com/assets/19897222/17392379/9b97257a-5a4f-11e6-84af-8e1c09817ab3.png)

The number of ST in Web and DB are first grouped by their affiliate network the similarity ratio and differences for the 2 data sets are calculated. 

![image](https://cloud.githubusercontent.com/assets/19897222/17392389/abee3ac6-5a4f-11e6-933a-971f3c4787d8.png)

This table shows the number of missing ST for each merchant. Merchants with no missing ST are not shown.

Findings
---------













