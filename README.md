# KENYA CROPS REPORT

## Project Overview 

Field officers have compiled a season's records for 500 smallholder farmers across Kenya : what they plantd,where ,on how many acres ,what it yielded ,what it sold for and what it cost.We would like to use the information to better understand how crops are performing in different seasons with different planting techniques and identify areas that require attention

## Project Objective 

The objective of this assessment is to create a Power BI solution that shows which crops ,counties and practises that make money and understand different overall performance of different crops and investigate factors contributing to that performance.Management should be able to understand sales and revenue performance,costs and profitability ,crop performance,farmers performance,geographic performance,seasons performance and unusual area that requirre further investigation

## Dataset

Our Crops dataset had 20 columns and 500 rows.Each of the 500 rows showed farmers details like their counties ,farming and crodetails together with total revenue and costs

|Entity | Fields |
|:------|:-------|
|Farming| Fertilizer Used, Irrigation Method , Pestcontrol , Soil Type , SoilID , Weather Impact |
|Locations | County ,LocationID, Region |
|Farmer | Farmer Contact , Name |
|Crops | Crop Type , Crop Variety ,CropID,Planted Acres,Season, Yield |

Apart from Farmer Name which is unique ,the rest of the dimensio tables we will have to create our very own primary keys .We are going to create four dimensional tables namely 

- DimFarming - This dimensional table will tells more about our techniques our farmers used.It contains fields like fertilizer used ,irrigation methos, pestcontrol and so on and so forth.We will create our primary keys to connect to the facts table 
- DimLocations - Locations table will tells us more about the region and counties these crops were grown and further showing region and counties farmers are from 
- DimCrops - Dimensional table crops with fields like crop type, crop variety,planted acres, season, yield will tell us more information about the crops,what type of variety is potatoes grown by Farmer50,how many acres of wheat were planted in Kiambu.Generally DimCrops tells us more about the crops

## Data Quality Audit 

|Issue | Columns Affected | Solution | Reason |
|:-----|:-----------------|:---------|:-------|
|Errors, N/A , Blanks | Planted Acres , Market Price , Revenue , Profit , Crop TYpe, Irrigation ,Crop Variety , Season , Yield , Counties , Cost of Production , Planting Date , Harvesting Date , Soil Type , Fertiliser Used , Pest Control, Weather Impact | Changed all errors, N/As, Blanks to Not Provided for all non monetary columns and changed name to nulls for monetary and date columns |We honestly cant delete rows because of blanks because we will be loosing crucial data and again cant just add information to our blanks because that again will be corrupting data|

For the most part of our data we just had to fix the errors and blanks because generally our data was quite okay 

## Data Modelling Approach

The supplied dataset is a flat table. We designed a star schema as our appropriate data model to enable time intelligence functions and even manipulation of data later in power BI.From the dataset we made 4 different dimensional tables and connected them to one fact table 
Below is an illustration of our modelling 

<img width="1520" height="1010" alt="Image" src="https://github.com/user-attachments/assets/d68a5411-f8e8-43cf-8817-7e7ac297d0fc" />

## DAX Functions 

The dataset wanted us to answer different managerial questions.Below are some of the questions :

- Which crop and county combination is most profitable per acre, and which loses money?
- Do irrigated or fertilised plots earn more profit than those without?
- What three actions would you recommend to the programme director, and which measures support each?

```dax 
Total Revenue = SUM(FactsCrops[Revenue(KES)])
```

```dax
Total Yield = SUM(FactsCrops[Yield(Kg)])
```

```dax 
Average Market Price = Average(FactsCrops[Market Price(KES/Kg)]
```

```dax 
Revenue Per Acre = DIVIDE([Total Revenue ] , SUM(DimCrops[Planted Area(Acres)])
```

```dax 
DATE = CALENDAR(DATE(2023,01,01),DATE(2023,12,31))
```
We do create a date table to enable us perform time intelligence functions like SAMEPERIODLASTYEAR, TOTALYTD , DATEDDIFF , DATEDADD ...


## Executive Dashboard 

<img width="1520" height="1010" alt="Image" src="https://github.com/user-attachments/assets/b49cc99f-3da3-4010-9ac0-c6461a908cf3" />

RECOMMENDATIONS

The following insights were made from our Crops data :
Not provided crop type had the most revenue of 160.41M followed by Rice with a revenue of 133.01M and Sorghum closing our top three with revenue of 121.12M 
Nyeri had the most revenue of   162.05 M   followed by Nairobi with a revenue of  132.89M  and Nakuru with revenue of  112.18M
There is a strong correlation between profit and yield as compared to profit and average market price
Tea and rice bore the most cost for crops grown
  

Looking at the data ,we had the following recommendations to make :
Most of our crops performed well without the need of modern agricultural practices because we are yielding over 400M from crops that used no fertilizers, we need to investigate and know why is this case, do some of these crops require no fertilizer because we can have our farmers cutting cost on fertilizers although this is not the case for all the crops and hence we should investigate and know which crop yield best with urea, which one yield best with organic ....

Encourage our farmers to use organic pest control as compared to chemical because organic controls yield even more crops per acre with a whooping 71 %

We can have farmers planting wheat and rice using more of hybrid crop variety and those growing potatoes and cassava using organic variety. Different crops perform better with different varieties and hence we should dive deeper and know what variety is best suitable for certain crops

Lets us do investigate what does "Not Provided " refer to because we are missing out on very important data for instance crops that had their type as not provided had the most revenue


