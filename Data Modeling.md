# <p align="center" style="margin-top: 0px;"> 🔩 ADVENTURE WORKS PRODUCTION ANALYSIS 🔩
## <p align="center"> Data Modeling

I built a many-to-many data model relationship for this project 

![The data model](https://github.com/Gemmahhh/Adventure-Works-Production-Analysis/blob/main/images/The%20data%20model%20relationship.JPG)

The tables below showcase the relationships used in this analysis 

<strong> WORK ORDER ROUTING TABLE </strong>
Table it has relationships with |	Columns used to establish the relationship |
-- | -- |
Product table | Product ID |
Work order table | Work Order ID |
Calendar table | Actual Start date |
Location table | Location ID |

<br> </br>
<strong> PRODUCT TABLE </strong>
Table it has relationships with |	Columns used to establish the relationship |
-- | -- |
Bill of Materials table | Product ID |
Work order table | Product ID |
Work Order Routing table | Product ID |

<br> </br>
<strong> LOCATION TABLE </strong>
Table it has relationships with |	Columns used to establish the relationship |
-- | -- |
Work Order Routing table | Location ID |

<br> </br>
<strong> WORK ORDER TABLE </strong>
Table it has relationships with |	Columns used to establish the relationship |
-- | -- |
Product table | Product ID |
Work order table | Work Order ID |
Calendar table | Start date |
Scrapped Reason table | ScrappedReason ID |

<br> </br>
<strong> BILL OF MATERIALS TABLE </strong>
Table it has relationships with |	Columns used to establish the relationship |
-- | -- |
Product table | Component ID |
Product table | Product Assembly ID |

<br> </br>
<strong> CALENDER TABLE </strong>
Table it has relationships with |	Columns used to establish the relationship |
-- | -- |
Work order routing table | Date |
Work order table | Date |

<br> </br>
<strong> SCRAPPED REASON TABLE </strong>
Table it has relationships with |	Columns used to establish the relationship |
-- | -- |
Work order table | Scrapped Reason ID |
