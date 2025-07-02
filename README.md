# DSA-Amazon-Project-Review-Analysis
I was tasked with the responsibility of analyzing product and customer review data to generate insights that can guide product improvement, marketing strategies, and customer engagement.

# Amazon Product Review Dataset: Data Cleaning, Analysis & Dashboard Insights
![Amazon Dashboard Visualization](https://github.com/user-attachments/assets/d7fea85b-1e2e-4c81-9c9e-28320a7a6db9)

## Table of Contents
- [Project Overview](#project-overview)
- [Step 1: Data Cleaning Using Power Query](#step-1-data-cleaning-using-power-query)
  - [1. Load Data into Power Query](#1-load-data-into-power-query)
- [Step 2: Data Analysis Using Pivot Tables](#step-2-data-analysis-using-pivot-tables--see-attached-visualization-dashboard-for-results)
- [Dashboard Development](#dashboard-development)
- [Key Findings](#key-findings)
- [Recommendations](#recommendations)
  
## Project Overview
The dataset comprises 1,465 Amazon products across 16 columns, containing aggregated product and review information. Before performing any analysis, a comprehensive data cleaning process was conducted using Power Query in Excel, followed by insightful analysis and dashboard visualization using pivot tables and charts.

**Data Sources:**  
The primary data source utilized in this analysis is Amazon Case Study.xlsx, an open-source dataset that is freely available for download from platforms such as Kaggle, LMS platform or other public data repositories.   

**Tools Used:**  
- Microsoft Excel for Data Cleaning and Visualization [Download Here](https://www.microsoft.com/en-us/microsoft-365/download-office) 
- Power Query for ETL processes
- Pivot Table for analysis  

## Step 1: Data Cleaning Using Power Query

### 1. Load Data into Power Query
- Load the dataset by selecting the range in Excel and navigating to:
  `Data → Get & Transform Data → From Table/Range`
- Click `OK` to open the Power Query Editor.

## 2. Cleaning Multi-Value Columns
### A. Remove Extra Spaces
- Select columns like user_ids
- Use `Transform → Format → Trim`
- Replace multiple spaces:  
  `Transform → Replace Values → Find: ", " → Replace with: ","`

### B. Handle Empty Values
- Replace "NA", "NULL", or blanks:  
  `Right-click column → Replace Values → Replace with empty values`

### C. Split Comma-Separated Fields
- For columns:  
  `Transform → Split Column → By Delimiter (Comma) → "Each occurrence" → Columns`

### 3. Remove Duplicates
-	For key fields like review_id, remove duplicates by
  -	Right-click column → Remove Duplicates

### 4. Standardize Text Fields
-	Remove line breaks in fields like review_content:
    -	Replace `#(lf)` or `#(cr)` with space
-	Convert text to lowercase or capitalize as required:
    -	Use `Transform → Format → Lowercase / Capitalize` Each Word

**Column-Specific Cleaning**
### A. review_title
-	Trim spaces and replace `", "` with a temporary delimiter `"|"`.
-	Replace internal commas with `"; "` to preserve title integrity.
-	Replace placeholders like `"NA"` or `"-"` with blanks.
-	Split by `"|"` into rows, then restore original commas.
-	Capitalize each word and remove unwanted characters.
  
### B. user_name
-	Trim whitespace and standardize delimiters.
-	Replace placeholders with blanks.
-	Split names by comma into individual rows.
-	Capitalize names and remove special characters.
-	Remove duplicate user entries.
  
### C. category

-	Split hierarchical values using delimiter `|` into:
    -	`MainCategory, SubCategory1, SubCategory2`.
-	Trim whitespace, capitalize, and standardize category names.
-	Replace null values with `"Uncategorized"`.
-	Consolidate similar entries (e.g., "Electronic" → "Electronics").

**Product Categories Outcome**
-	Electronics
-	Home & Kitchen
-	Computers & Accessories
-	Musical Instruments
-	Office Products
-	Home Improvement
-	Car & Motorbike
-	Toys & Games
-	Health & Personal Care

### D. product_name
•	Trim spaces, remove line breaks, and capitalize product names.
•	Optionally shorten long names using a custom column formula:
  `= Text.Start([product_name], 30) & "...".`

**Other Data Preparation Tasks**

-	Convert actual_price, discounted_price, and rating columns from text to numerical types.
-	Handle missing values in rating_count by replacing them with 0.
-	Create derived columns for easier analysis:
    -	high_discount: = IF(discount_percentage >= 0.5, 1, 0)
    -	potential_revenue: = actual_price * rating_count
    -	rating_x_count: = rating * rating_count
    -	price_bucket:
    -	= `IF([actual_price] < 200, "Under 200"`,
        -	`IF([actual_price] <= 500, "200–500"`,
        -	`IF([actual_price] > 500, "Above 500", "Blank")))`

## Step 2: Data Analysis Using Pivot Tables- see attached Visualization Dashboard for results

### 1.	Average Discount by Category:
-	Result: 46%
-	Rows: category | Values: Average of discount_percentage
  
### 2.	Products per Category:
-	Result: 73,614
-	Rows: category | Values: Count of product_id
  
### 3.	Total Reviews per Category:
-	Result: 1,029,234,871
-	Values: Sum of rating_count
  
### 4.	Highest Rated Products:
-	E.g., Syncwire Ltg To USB Cable, Amazon Basics Wireless Mouse, Redtech USB-C Cable
-	Rating: 5.0
  
### 5.	Average Actual vs Discounted Price by Category:
-	Avg Actual: £4,491 | Avg Discounted: £2,473

### 6.	Top Reviewed Products:
-	E.g., Aircase Laptop Bag, Spigen Screen Protector
-	Review Count: 192
  
### 7.	Products with ≥50% Discount:
-	Count: 32,767
  
### 8.	Rating Distribution:
-	3.0: 193 | 4.0: 8,296 | 5.0: 90
  
### 9.	Total Potential Revenue:
-	Sum of actual_price * rating_count per category
  
### 10.	Unique Products by Price Range:
-	Buckets: Under 200, 200–500, Above 500
  
### 11.	Rating vs Discount Relationship:
-	Use a scatter plot:
    -	X-axis: discount_percentage
    -	Y-axis: rating
      
### 12.	Products with <1,000 Reviews:
-	Use a filter or formula: =IF(rating_count < 1000, 1, 0)
  
### 13.	Categories with Highest Discounts:
-	Use Pivot Table: Max of discount_percentage
  
### 14.	Top 5 Products by Rating × Reviews:
-	Use rating * rating_count to rank

## Dashboard Development
### Key Metrics Displayed:
-	Total potential revenue
-	Average product rating
-	Total reviews
-	Count of products
-	Products with ≥50% discount
-	Products with ≥1000 reviews
  
### Visualizations Included:
-	Column Charts:
    -	Average discount by category
    -	Product count per category
    -	Reviews by product
    -	Price comparisons by category
    -	Potential revenue per category
-	Pie Chart: Discount percentage by category
-	Doughnut Chart: Unique products by price range
-	Scatter Plot: Rating vs Discount
-	Column Chart: Top products by rating × reviews
-	Picture Display: Highest-rated products
-	Interactive Filters: Category, Price Range

## Key Findings

### Top Insights
1. **Revenue Potential**: Computers & Accessories generates the highest potential revenue (£3,815.45B)
2. **Discount Trends**: Average discount across categories is 46%, with highest discounts in Home Improvement (57%)
3. **Product Ratings**: Average product rating is 4.08, with top-rated products achieving 5.0
4. **Review Volume**: Electronics has the highest review count (509M reviews)
5. **High-Discount Products**: 32,767 products have ≥50% discount

### Recommendations
- **Focus Marketing** on high-rated products in Computers & Accessories and Electronics
- **Monitor Pricing** in Home Improvement where discounts are deepest
- **Improve Engagement** for products with <1,000 reviews to boost visibility
- **Leverage Top Products** like Syncwire USB Cable and Amazon Basics Mouse as benchmarks



