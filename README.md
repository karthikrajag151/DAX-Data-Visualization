# Power BI Project: DAX & Data Visualization – E-Commerce Sales Analysis

## 📌 Project Overview

This project focuses on analyzing an E-Commerce Sales Dataset using **Microsoft Power BI, DAX (Data Analysis Expressions), and interactive data visualizations**.

As an aspiring Data Analyst, I developed this project to strengthen my skills in data analysis, business intelligence, DAX calculations, and dashboard development. Building on the data transformation and data modeling completed in the previous assignment, this project focuses on creating calculated columns, developing analytical measures, and designing interactive visualizations to evaluate sales performance, profitability, sales targets, and regional trends.

The final Power BI report provides a consolidated view of key business metrics to support data-driven decision-making.

## 🎯 Project Objectives

- Create calculated columns using DAX to derive meaningful business attributes.
- Develop DAX measures to calculate order counts, average profit, and year-to-date sales.
- Compare actual sales performance against business targets.
- Analyze sales and profit trends across categories, sub-categories, months, and states.
- Visualize relationships between profit and quantity sold.
- Identify geographical sales patterns across different cities.
- Build an interactive and well-structured Power BI dashboard.
- Translate analytical results into actionable business insights.

## 📂 Dataset Description

The project uses three datasets representing order transactions, order details, and sales targets.

### 1. List of Orders

Contains order-level information about customers, locations, sales categories, and profitability.

| Column | Description |
|---|---|
| Order ID | Unique identifier for an order |
| Order Date | Date the order was placed |
| Customer Name | Name of the customer |
| City | City associated with the order |
| State | State associated with the order |
| Category | Product category |
| Amount | Sales amount associated with the order |
| Profit | Profit generated from the order |

### 2. Order Details

Contains product-level information, including quantities, sub-categories, and financial values.

| Column | Description |
|---|---|
| Order ID | Identifier used to associate order details with orders |
| Category | Main product category |
| Sub-Category | More specific product classification |
| Quantity | Number of units sold |
| Amount | Sales amount recorded in the dataset |
| Profit | Profit generated from the order details |

### 3. Sales Target

Contains monthly sales targets for different product categories.

| Column | Description |
|---|---|
| Category | Product category |
| Month of Order Date | Month associated with the sales target |
| Target | Target sales amount for the category and month |

**Data modeling:** The relationships created in the previous assignment are retained to support analysis across the datasets. Appropriate relationship cardinality, filter direction, and date handling are important for accurate calculations.

## 🛠️ Tools and Technologies

- **Microsoft Power BI Desktop** – Report development and dashboard creation
- **DAX (Data Analysis Expressions)** – Calculated columns and measures
- **Power Query Editor** – Data preparation inherited from the previous assignment
- **Data Modeling** – Relationships between orders, order details, and sales targets
- **Data Visualization** – Interactive charts, cards, maps, and matrices
- **GitHub** – Project documentation and portfolio management

## 🧮 DAX Calculations

### 1. Calculated Columns

#### A. Category Type

Combines the product category and sub-category into a single descriptive column in the Order Details table.

```dax
Category Type =
'Order Details'[Category]
    & " - "
    & 'Order Details'[Sub-Category]
```

**Purpose:** Provides a combined product classification for filtering, grouping, and visual analysis.

#### B. Revenue per Order

Calculates revenue using the Amount and Quantity columns, as specified in the assignment.

```dax
Revenue per Order =
'Order Details'[Amount]
    * 'Order Details'[Quantity]
```

**Purpose:** Creates a derived revenue value for each row in the Order Details table.

**Note:** Confirm the meaning of the Amount column before interpreting this metric. If Amount already represents the total sales value for a row, multiplying it by Quantity would double-count quantity. In that case, use Amount directly as the revenue value.

#### C. Sales Category

Classifies each row as Above Average or Below Average based on its Amount compared with the overall average Amount in the Order Details table.

```dax
Sales Category =
VAR AverageAmount =
    CALCULATE(
        AVERAGE('Order Details'[Amount]),
        REMOVEFILTERS('Order Details')
    )
RETURN
    IF(
        'Order Details'[Amount] >= AverageAmount,
        "Above Average",
        "Below Average"
    )
```

**Purpose:** Segments sales records according to their performance relative to the overall average amount. Records equal to the average are classified as Above Average.

### 2. Calculated Measures

#### A. Order Count

Counts distinct order IDs in the Order Details table.

```dax
Order Count =
DISTINCTCOUNT('Order Details'[Order ID])
```

**Purpose:** Measures the number of unique orders represented in the Order Details table.

#### B. Average Profit in Delhi

Calculates the average profit for orders associated with Delhi.

```dax
Average Profit in Delhi =
CALCULATE(
    AVERAGE('List of Orders'[Profit]),
    'List of Orders'[City] = "Delhi"
)
```

**Purpose:** Evaluates the average order-level profit for Delhi.

#### C. Year-to-Date (YTD) Sales

Calculates cumulative sales from the beginning of the year through the current date in the report's date context.

```dax
YTD Sales =
TOTALYTD(
    SUM('List of Orders'[Amount]),
    'Date'[Date]
)
```

**Purpose:** Tracks cumulative sales performance throughout the year.

**Requirement:** The example assumes that a properly configured Date table named `Date` exists, with a continuous date column marked as the date table. The Date table must have an appropriate relationship with the order dates. If your model does not contain this table, create one and establish the relationship before using this measure.

## 📊 Data Visualizations

The report includes the following visualizations to analyze different aspects of e-commerce performance.

| No. | Visualization | Chart Type | Business Purpose |
|---|---|---|---|
| 1 | Sales Target Achievement by Category | Clustered Column Chart | Compares actual sales and targets across product categories. |
| 2 | Maximum Profit Margin by Sub-Category | Donut Chart | Displays the distribution of maximum profit-margin values across sub-categories. |
| 3 | Monthly Sales Trend | Line Chart | Identifies monthly sales trends and changes over time. |
| 4 | Profit vs. Quantity by Sub-Category | Scatter Chart | Examines the relationship between quantity sold and profit. |
| 5 | Total Sales Amount vs. Target | Card Visuals | Provides a quick comparison of actual sales and sales targets. |
| 6 | Minimum Target by Segment | Multi-row Card | Displays minimum target values for the relevant categories or segments. |
| 7 | Sales Performance Matrix | Matrix | Compares actual sales and targets across categories and months. |
| 8 | Geographic Sales Analysis | Map | Shows sales distribution across cities. |
| 9 | Sales Distribution by Sub-Category | Treemap | Highlights the relative contribution of product sub-categories to sales. |
| 10 | Order Count by State | Funnel Chart | Compares order counts across states. |

### Visualization Details

#### Sales Target Achievement by Category
Compares actual sales with sales targets for each product category. It helps identify categories that meet, exceed, or fall short of their targets.

#### Maximum Profit Margin by Sub-Category
Uses a donut chart to compare maximum profit-margin values across product sub-categories. Profit margin should be calculated as profit divided by sales amount, with suitable handling for zero or blank sales values. Since maximum margin can be sensitive to individual records, interpret this chart alongside total profit and sales.

#### Monthly Sales Trend
Displays sales over time using a line chart. It helps identify high-performing months, low-performing periods, and potential seasonal patterns.

#### Profit and Quantity by Sub-Category
Uses a scatter chart to compare quantity sold with profit for different sub-categories. It helps identify high-volume products, profitable sub-categories, and products with high sales volume but low profitability.

#### Sales Amount and Target Cards
Displays total actual sales and total sales target in separate cards, making it easy to assess overall target performance.

#### Minimum Target by Segment
Uses a multi-row card to show the minimum target for each relevant category or segment.

#### Sales Performance Matrix
Presents sales and target values by category and month. It supports detailed comparisons, highlights performance gaps, and helps identify periods requiring further investigation.

#### Geographic Sales Analysis
Uses a map to visualize sales by city and identify regional differences in sales performance.

#### Sales Distribution by Sub-Category
Uses a treemap to display the relative contribution of each sub-category to total sales. Larger rectangles represent higher sales values.

#### Order Count Analysis by State
Uses a funnel chart to compare order counts across states. It helps identify states with higher and lower order volumes, although a bar chart may be more suitable for precise comparisons between independent states.

## 📈 Business Questions Addressed

This project is designed to answer the following business questions:

- Which product categories perform best against their sales targets?
- How do monthly sales change over time?
- Which sub-categories contribute to sales and profitability?
- Is there a relationship between quantity sold and profit?
- What is the average profit generated by orders in Delhi?
- How many unique orders are represented in the dataset?
- Which cities and states contribute to regional sales performance?
- How do actual sales compare with monthly category targets?
- Which categories and periods require additional attention to achieve sales goals?

## 💡 Business Insights and Recommendations

The following insights can be investigated using the completed report. Actual findings should be added after validating the results in Power BI.

- **Target performance:** Identify categories consistently exceeding their targets and investigate the reasons behind their performance.
- **Sales trends:** Examine monthly peaks and declines to support inventory planning and promotional decisions.
- **Profitability:** Compare profit and sales volume to identify sub-categories that generate strong profit despite lower quantities sold.
- **Regional performance:** Identify cities and states with strong or weak sales contributions and investigate local demand.
- **Product mix:** Use the treemap and category comparisons to identify important contributors to overall sales.
- **Target gaps:** Use the matrix to locate categories and months where actual sales are below target and recommend targeted sales initiatives.

## 📁 Project Structure

The GitHub repository can be organized as follows:

```text
Power-BI-DAX-Data-Visualization/
│
├── DAX & Data Visualization.pbix
├── README.md
│
├── screenshots/
│   ├── dashboard-overview.png
│   ├── dax-calculated-columns.png
│   ├── dax-measures.png
│   ├── sales-target-analysis.png
│   ├── monthly-sales-trend.png
│   ├── profitability-analysis.png
│   ├── geographic-sales-analysis.png
│   └── sales-performance-matrix.png
│
└── documentation/
    └── DAX-and-Visualization-Report.pdf
```

*The folders and screenshot filenames above are suggested. Add the files once they have been created and verified.*

## 📦 Deliverables

The project deliverables include:

1. **Power BI report (.pbix):** Contains the data model, calculated columns, DAX measures, visualizations, and report layout.
2. **PDF documentation:** Contains screenshots of DAX formulas, completed visualizations, the dashboard layout, and brief explanations of each visual.
3. **GitHub README:** Documents the project objectives, dataset structure, calculations, visualizations, and analytical approach.

## 🚀 Skills Demonstrated

- DAX calculated columns and measures
- Aggregation and filter-context management
- Time intelligence and YTD analysis
- Data modeling and table relationships
- Sales and profitability analysis
- Target achievement analysis
- Interactive dashboard development
- Data storytelling and business interpretation
- Analytical problem-solving
- Technical documentation using GitHub

## 🔍 Conclusion

This project demonstrates how Power BI and DAX can transform e-commerce sales data into meaningful business metrics and interactive reports. By combining calculated columns, analytical measures, and multiple visualization types, the report supports the evaluation of sales performance, profitability, target achievement, and regional trends.

As an aspiring Data Analyst, this project represents a step toward building practical skills in business intelligence, analytical reporting, and data-driven decision-making.

## 👤 Author

**Aspiring Data Analyst**

Interested in data analytics, business intelligence, data visualization, and transforming raw data into actionable business insights.

## 📌 Project Status

Completed as part of the **Data Analytics (DA) – Module 2: Power BI Assignment 2 – DAX & Data Visualization** learning program.

---

*This project is intended for educational and portfolio purposes. Business insights and recommendations should be finalized after validating the actual Power BI report results.*
# DAX-Data-Visualization
