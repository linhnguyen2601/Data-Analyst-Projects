# Coffee Bean Sales Dashboard

![image](https://github.com/linhnguyen2601/Excel-Projects/assets/166676829/b7d7f7d3-dc5f-4e46-94d0-7ea0b99362e2)

## 1. Introduction

### 1.1. Business Requirements

#### Key Analysis Areas:

Customer Analysis:

- Demographic Insights: Identify key demographics of customers (age, location, etc.) and their purchasing behavior.
- Loyalty Program Impact: Evaluate the impact of the loyalty card program on sales and customer retention.
- Customer Segmentation: Segment customers based on purchasing patterns, frequency, and average order value to tailor marketing strategies.

Sales Performance:

- Overall Sales Trends: Analyze monthly and quarterly sales trends to identify peak sales periods and seasonal variations.
- Product Sales Analysis: Determine the best and worst-selling products, analyzing the impact of coffee type, roast type, and size on sales performance.
- Order Patterns: Examine the average order value, order frequency, and typical order quantities.

Product Performance:

- Product Popularity: Rank products by sales volume and revenue to identify top-performing items.
- Price Sensitivity: Analyze how changes in product pricing affect sales volume and revenue.
- Inventory Management: Identify fast-moving and slow-moving products to optimize inventory levels.

### 1.2. Dataset overview

The Coffee Sales Performance dataset is structured into three interconnected tables: Customers, Products, and Orders.

- The Customers table includes detailed information about each customer, such as customer ID, customer name, demographics (location), contact information, and whether the customer owns a loyalty card.

- The Products table provides specifics about the coffee products offered, including product ID, coffee type (e.g., Arabica or Robusta), roast type, size, and unit price.

- The Orders table captures transactional data, detailing order ID, order date, customer ID, product ID and quantity.

This comprehensive dataset enables in-depth analysis of sales trends, customer behavior, and product performance, offering valuable insights to drive strategic business decisions and optimize sales outcomes.

## 2. Data processing

**I gathered the customer data using XLOOKUP:**

CUSTOMER NAME:
```
= XLOOKUP($C$2, customers!$A$1:$A$1001, customers!$B$1:$B$1001,,0)
```

EMAIL:
```
= IF(XLOOKUP(C2, customers!$A$1:$A$1001, customers!$C$1:$C$1001,,0)=0, "", XLOOKUP(C2, customers!$A$1:$A$1001, customers!$C$1:$C$1001,,0))
```

COUNTRY:
```
=XLOOKUP(C2, customers!$A$1:$A$1001, customers!$G$1:$G$1001,,0)
```

LOYALTY CARD
```
= XLOOKUP([@[Customer ID]], customers!$A$1:$A$1001, customers!$I$1:$I$1001,,0)
```

I gathered the product data using INDEX() MATCH()

COFFEE TYPE:
```
=INDEX(products!$A$1:$G$49, MATCH(orders!$D2, products!$A$1:$A$49,0), MATCH(I$1, products!$A$1:$E$1, 0))
```

ROAST TYPE:
```
=INDEX(products!$A$1:$G$49, MATCH(orders!$D2, products!$A$1:$A$49,0), MATCH(J$1, products!$A$1:$E$1, 0))
```

SIZE
```
=INDEX(products!$A$1:$G$49, MATCH(orders!$D2, products!$A$1:$A$49,0), MATCH(K$1, products!$A$1:$E$1, 0))
```

UNIT PRICE:
```
=INDEX(products!$A$1:$G$49, MATCH(orders!$D2, products!$A$1:$A$49,0), MATCH(L$1, products!$A$1:$E$1, 0))
```

Then I changed the name of Coffee Type Name:
```
=IF(I2="Rob", "Robusta", IF(I2 = "Exc", "Excelsa", IF(I2="Ara", "Arabica", "Liberica")))
```

and Roast Type Name:
```
=IF(J2 = "M", "Medium", IF(J2 = "L", "Light", "Dark"))
```


```
