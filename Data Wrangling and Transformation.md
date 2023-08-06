# <p align="center" style="margin-top: 0px;"> 🔩 ADVENTURE WORKS PRODUCTION ANALYSIS 🔩
## <p align="center"> Data Wrangling and Transformation

### For this section, my main aim was to get the datasets ready for modeling and analysis. 

#### Steps Taken:
* I assessed the data on Microsoft SQL Server using it's dictionary and then loaded it into Power BI (Power Query) for transformation
  
* In Power query, I removed unnecessary columns from the tables

  #### COLUMNS REMOVED
  No |	Column Name |
  -- | -- |
  1 |	Color (Product table) |
  2 |	ProductSubCatID (Product table) |
  3 |	ProductModelID (Product table) |
  4 |	Rowguide (Product table) |
  5 |	Modified Date (Product table) |
  6 |	Rowguide (Location table) |
  7 |	Availability (Location table) |
  8 |	Rowguide (Work Order Routing table) |
  9 |	Modified Date (Work Order Routing table) |
  10 |	Rowguide (Scrap Reason table) |
  11 |	Rowguide (Bill Of Material table) |

* For all the Modified date columns across all the tables chosen for the analysis, I separated the 'date' and 'time' into different columns
 
* I created extra columns which was used for the Key Influencers chart in the Overview table, the columns are - Delay and Scrapped.
  * The delay column simply identifies if a row has any digit above 0 in the "Delay_days" table then assigns "Delay" else it assigns "No Delay"
  * The scrapped column identifies if a row has any digit above 0 in the "ScrapReasonID" table then assigns "Scrapped" else it assigns "Not Scrapped"

* I created an extra column to find out the difference between the "Scheduled Start" date and "Actual Start" date then gave it a column name "Delay in Start days"

* Then I created another column that outputs the difference between the "Actual End date" and "Actual Start date" and named the column "Production days"

In Power BI, the visualization pane, I created the Calender table using the calender auto DAX formula ie 

```dax
  Calendar = CALENDARAUTO()
```
Then I created the following columns in the Calender table 
- Month, Quarter, Year, and Month Number(I used this column to sort the entire table)
  ```dax
  Month = FORMAT('Calendar'[Date],"mmm")
  Quarter = FORMAT('Calendar'[Date], "\QQ")
  Year = FORMAT('Calendar'[Date],"yyyy")
  Month number = Month('Calendar'[Date])  

After I was done with the Calender table, I created the following measures
* <strong>Order Measure</strong>: This measure sums up the Orderqty column and it's used to create other measures needed for this analysis.
  ```dax
  Order Measure = CALCULATE(SUM('ProductionWorkOrder'[OrderQty]))

* <strong> Previous Month Order</strong>:This measure simply getd the value of the order quantity in the previous month
   ```dax
  Previous Month Order = CALCULATE([Order Measure], PREVIOUSMONTH('Calendar'[Date]))

* <strong> Order MOM Variance </strong>: This measure displays the difference between the total number of orders in a month and the total number of orders in the previous month
  ```dax
  Order MOM Variance = [Order Measure] - [Previous Month Order]

* <strong> Order MOM% Variance </strong>: This measure simply displays the percentage of the order MOM Variance
  ```dax
  Order MOM% Variance = DIVIDE([Order MOM Variance],[Previous Month Order],0)

* <strong> OrderQty Measure </strong>: This measure was used to have a measure version of the Orderqty column in the Work Order table. The measure was used to create other measures needed for this analysis
  '''dax
  OrderQty Measure = SUM('ProductionWorkOrder'[OrderQty])

* <strong> Order SPLY </strong>: Using the SAMEPERIODLASTYEAR function in DAX, I extracted the orders for the previous year
  ```dax
  Order SPLY = CALCULATE ([OrderQty Measure], SAMEPERIODLASTYEAR('Calendar'[Date]))

* <strong> MOM% OrderQty </strong>: This measure simply gets the percentage of the Month on Month Variance for the orders
  ```dax
  MOM% Orderqty = VAR __PREV_MONTH = CALCULATE(
    SUM(
        ProductionWorkOrder[OrderQty]
    ),
    DATEADD(
        'Calendar'[Date],
        -1,
        MONTH
    )
  )
  RETURN 
    DIVIDE(
        SUM(
            ProductionWorkOrder[OrderQty]
        ),
        
        __PREV_MONTH
      )
