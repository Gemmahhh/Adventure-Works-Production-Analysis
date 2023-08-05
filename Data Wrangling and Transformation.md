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
  * The delay table simply identifies if a row has any digit above 0 in the "Delay_days" table then assigns "S
