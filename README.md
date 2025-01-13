# CREDIT CARD FINANCIAL ANALYSIS DASHBOARD


## Problem Statement

The credit card division has been experiencing fluctuations in customer spending, payment behaviors, and default rates. Current reporting methods are fragmented and lack the ability to provide actionable insights. This project aims to consolidate data from various sources, enabling service providers to make informed decisions regarding marketing strategies, risk assessment, and customer engagement.

This project will enable the credit card division to make data-driven decisions, enhance customer satisfaction, and optimize financial performance.


### Steps followed 

- Step 1 : Create tables in the SQL according to the csv file. Import the CSV file to SQL
- Step 2 : Connect the SQL database to the Power Bi editor.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset". 
- Step 4 : Visual filters (Slicers) were added for four fields named "Quater", "Gender", "Income Type" , "Card Category" & "Week Start Date".
- Step 5 : Four card visuals were added to the canvas,representing "Sum of Revenue" , "Total Interest", "Total Income" & "Average Customer".
- Step 6 : Multiple Bar Charts were added to represent different measures such as Top 5 states, Age Group, Education Level & Revenue generation through many types.  
- Step 7 : Tables and Line Chart for other important calculations that can be filtered through slicers or filters.
- Step 8 : Calculated column was created in which, customers were grouped into various age groups.

for creating new column following DAX expression was written;
       
        Age Group = SWITCH(
    True(),
    customer_detail[Customer_Age]<30,"20-30",
    customer_detail[Customer_Age]>=30 && 'customer_detail'[Customer_Age]<40,"30-40",
    customer_detail[Customer_Age]>=40 && 'customer_detail'[Customer_Age]<50,"40-50",
    customer_detail[Customer_Age]>=50 && 'customer_detail'[Customer_Age]<60,"50-60",
    customer_detail[Customer_Age]>=60,"60+",
    "unknown"
    )
        
Snap of new calculated column ,

![Screenshot (11)](https://github.com/user-attachments/assets/b352c4fc-929a-47cf-8e4e-73db38f88c1a)

        
- Step 9 :Calculated column was created in which, customers were grouped into three income groups
Following DAX expression was written for the same,

         Income Group = SWITCH(
      TRUE(),
      customer_detail[Income]<35000,"Low Income",
      customer_detail[Income]>=35000 && customer_detail[Income]<70000,
      "Med Income",customer_detail[Income]>=70000,
      "High Income",
      "unknown"
      )
        
        
Snap of new calculated column

![Screenshot (12)](https://github.com/user-attachments/assets/df298daa-9e60-450f-b128-f7f891408c2b)



  Step 10 : Calculated column was created in which we got week number.

  Following DAX expression was written for the same, 

         Week num2 = WEEKNUM(credit_card_detail[Week_Start_Date])

 Snap of new calculated column

 ![Screenshot (14)](https://github.com/user-attachments/assets/89b6f70b-df12-4815-a95d-dfdd7687f9c6)


 Step 11 : A new measure is created to calculate sum of revenue.
 
 Following DAX expression was written to find total revenue,
 
    Revenue = credit_card_detail[Annual_Fees]+credit_card_detail[Total_Trans_Amt]+credit_card_detail[Interest_Earned] 

 A card visual was used to represent this value
 

 
![Screenshot (16)](https://github.com/user-attachments/assets/69e062c6-aede-4bb0-9a45-fa9972296ae4)

 
Step 12 : A new measure is created to get the Week On Week revenue(WOW) generation percentage.

 Following DAX expression was written to find the percentage of WOW,

      WoW_Revenue = DIVIDE([Current_week_revenue]-[Previous_week_revenue],[Previous_week_revenue])

A card visual was used to represent this value


![Screenshot (18)](https://github.com/user-attachments/assets/7d84adfb-45e7-4e50-98d9-595980e92cb6)
 
 - Step 13 : Two new measures were added for generation of Week On Week revenue. These two are used for the calculation of WOW.

  Following DAX expression was written to find out the Current Week Revenue,

     Current_week_revenue = CALCULATE(
    SUM(credit_card_detail[Revenue]),
    ALL(credit_card_detail),
    credit_card_detail[Week num2]=MAX(credit_card_detail[Week num2])
)

 Now the DAX expression for the Previous Week Revenue,

     Previous_week_revenue = CALCULATE(
    SUM(credit_card_detail[Revenue]),
    FILTER(
    ALL(credit_card_detail),
    credit_card_detail[Week num2]=MAX(credit_card_detail[Week num2])-1
))
 
 

# Snapshots of Dashboard 

## Transaction Report

![Screenshot (19)](https://github.com/user-attachments/assets/deb5711e-d61b-48c1-b518-3c9c06a57f3b)


## Customer Report

 
![Screenshot (20)](https://github.com/user-attachments/assets/f6f675d5-9744-4e22-83f8-62fa295873d0)

# Insights

Double page report was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the dashboard;

###  Total Number of Customers = 10108

   Total Revenue generation (Male) = $30M (54.64 %)

   Total Revenue generation (Female) = $25M (45.36 %)

   Blue & Silver credit card are contributing to 93% of overall transactions.

   Total transaction amount is $46M

   TX, NY & CA is contributing to 68%. 
 

 ###  Some other insights
 
 ### Transaction methods
 
 1.1) 30.67 % customers pay by Chip.
 
 1.2) 63.12 % customers pay by swipe.
 
 1.3) 6.21 % customers pay by online method.
 
         thus, maximum customers pay by swipe method.
 
 ### Age Group
 
 2.1)  2.13 % customers belong to '20-30' age group.
 
 2.2)  18.19 % customers belong to '30-40' age group.
 
 2.3)  44.81 % customers belong to '40-50' age group.
 
 2.4)  29.61 % customers belong to '50-60' age group.

 2.5)  5.26 % customers belong to '60+' age group.
 
         thus, maximum customers belong to '40-50' age group.

3) Overall Delinquent rate is 6.06%

![Screenshot (22)](https://github.com/user-attachments/assets/4c5d0e18-279b-4867-af6f-9b0241458cdd)

4) Overall Activation rate is 57.5%

![Screenshot (24)](https://github.com/user-attachments/assets/bde2436f-8ca5-4f19-aff5-1800590ec0f9)

5) Blue Card Category has the highest percentage of Average Utilization Ratio among others.

![Screenshot (23)](https://github.com/user-attachments/assets/0235b0e4-4359-4cec-bedb-600a1c297370)

