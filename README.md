# Customer Lifetime Value Prediction

This project implements a Customer Lifetime Value (CLTV) prediction model using transaction data from an online retail company. The data set includes customer transactions and the goal is to calculate and segment customers based on their lifetime value. The following steps and calculations are implemented in the analysis:

## Data Set Overview

The data set used is from the **Online Retail II** data set available at [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Online+Retail+II). The transactions cover the period from 01/12/2009 to 09/12/2011 for a UK-based online retail company primarily selling gift-ware.

### Attributes in the Data Set:

- **InvoiceNo**: Invoice number. If the invoice starts with 'C', it indicates a cancellation.
- **StockCode**: Product code.
- **Description**: Name of the product.
- **Quantity**: Quantity of the product purchased in each transaction.
- **InvoiceDate**: Date and time of the transaction.
- **UnitPrice**: Price per unit of the product in GBP (£).
- **CustomerID**: Unique customer identifier.
- **Country**: Country of the customer.

## Key Steps and Calculations

### 1. Data Cleaning
- Removed transactions with a 'C' in the invoice number (indicating cancellations).
- Filtered out records with non-positive quantities and missing values.

### 2. Calculating Total Price
A new column, `TotalPrice`, is created by multiplying the `Quantity` by the `UnitPrice` for each transaction.

### 3. Aggregating Customer Data
For each customer, the following metrics are calculated:
- **Total Transaction**: Number of unique transactions made by the customer.
- **Total Unit**: Total number of units purchased by the customer.
- **Total Price**: Total amount spent by the customer.

### 4. Average Order Value (AOV)
The average order value for each customer is calculated as:
- **average_order_value** = `total_price / total_transaction`

### 5. Purchase Frequency
The purchase frequency is calculated as the number of transactions per customer divided by the total number of customers:
- **purchase_frequency** = `total_transaction / total_number_of_customers`

### 6. Repeat Rate and Churn Rate
- **Repeat Rate**: Percentage of customers who made more than one purchase.
- **Churn Rate**: Percentage of customers who only made one purchase.

### 7. Profit Margin
Assumed a 10% profit margin on each transaction:
- **profit_margin** = `total_price * 0.10`

### 8. Customer Value (CV)
The customer value is calculated by multiplying the **average order value** by the **purchase frequency**:
- **customer_value** = `average_order_value * purchase_frequency`

### 9. Customer Lifetime Value (CLTV)
The CLTV is calculated using the formula:
- **CLTV** = `(customer_value / churn_rate) * profit_margin`

### 10. Segmenting Customers
The customers are segmented into four quartiles (A, B, C, D) based on their CLTV values using the `qcut` function. Segment A represents the highest value customers, and segment D represents the lowest value customers.

## Final Output

- **Customer Lifetime Value (CLTV)** for each customer is calculated.
- **Customer segments** are created based on CLTV.
- A CSV file (`cltc_c.csv`) is saved containing the results.

## Example Output

Here is an example of how the customer data will look after segmentation:

| Customer ID | CLTV    | Segment |
|-------------|---------|---------|
| 18102      | 1000.0  | A       |
| 14646      | 950.0   | A       |
| 14156      | 930.0   | A       |
| 14911      | 890.0   | A       |
| 13694      | 850.0   | A       |

### Summary of Segments

- **Segment A**: High-value customers with the highest CLTV.
- **Segment B**: Mid-range customers.
- **Segment C**: Low-value customers.
- **Segment D**: Customers with the lowest CLTV.

## Requirements

- Python 3.x
- Libraries: `pandas`, `sklearn`

You can install the necessary libraries using the following:

```bash
pip install pandas sklearn
