# DSA-Amazon-Project-Review-Analysis
I was tasked with the responsibility of analyzing product and customer review data to generate insights that can guide product improvement, marketing strategies, and customer engagement.

# Amazon Product Review Dataset: Data Cleaning, Analysis & Dashboard Insights

## Project Overview
The dataset comprises 1,465 Amazon products across 16 columns, containing aggregated product and review information. Before performing any analysis, a comprehensive data cleaning process was conducted using Power Query in Excel, followed by insightful analysis and dashboard visualization using pivot tables and charts.

**Data Sources:**  
The primary data source utilized in this analysis is Amazon Case Study.xlsx, an open-source dataset that is freely available for download from platforms such as Kaggle, LMS platform or other public data repositories.   

**Tools Used:**  
- Microsoft Excel for Data Cleaning and Visualization  
- Power Query for ETL processes  

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
