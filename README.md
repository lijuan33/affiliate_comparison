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
-------------

**Features:**
  * `currency_convert`: converts amounts in various currencies to SGD
  * `clean_web_affiliate_name`: clean data in Web to match the data in DB
  * `clean_db_affiliate_name`: clean data in DB to match the data in Web

### Compare amount
-------------------

This method will compare the order amount and commission amount in Web data with the order amount and commission amount in DB data to give us the similarity ratio, difference and error rate.

#### Similarity ratio

This function gives us the ratio of similarity between the Web and DB's order amount and commission amount.
```
if (DB order amount < Web order amount) : 
    100 * (DB order amount / Web order amount)
 else:
    100 * (Web order amount / DB order amount)
    
if (DB commission amount < Web commission amount) :
    100 * (DB commission amount / Web commission amount)
else:
    100 * (Web commission amount / DB commission amount)
```
#### Difference

This function gives us the difference between the Web and DB's order and commission amount.
'''







