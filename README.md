# 📊 E-Commerce Sales Analysis using Power BI
## DAX & Data Visualization

## 📌 Project Overview

This project focuses on analyzing e-commerce sales performance using **Microsoft Power BI, DAX (Data Analysis Expressions), and interactive data visualizations**. As part of my Data Analytics learning journey, I worked with an e-commerce sales dataset to develop calculated columns, create analytical measures, and build interactive reports that help understand sales performance, profitability, order trends, and target achievement.

The project builds on the data transformation and data modeling tasks completed in the previous Power BI assignment. The existing data model is used to perform DAX calculations and develop meaningful business insights through visual storytelling.

This project demonstrates my foundational skills in data analysis, business intelligence, DAX calculations, and dashboard development as an aspiring Data Analyst.

## 🎯 Project Objectives

- Analyze e-commerce sales and profitability using Power BI.
- Create calculated columns to derive meaningful business attributes.
- Develop DAX measures for order count, average profit, and year-to-date sales.
- Compare actual sales against business targets across categories and months.
- Analyze sales and profit performance across product sub-categories.
- Identify geographic sales patterns across cities and states.
- Build interactive visualizations to communicate business performance.
- Present key performance indicators (KPIs) through a structured dashboard.

## 🗂️ Dataset Description

The project uses three datasets representing order information, product-level order details, and sales targets.

### 1. List of Orders

Contains order-level information about customers, locations, sales, and profitability.

**Attributes:**
- Order ID
- Order Date
- Customer Name
- City
- State
- Category
- Amount
- Profit

### 2. Order Details

Contains product category, sub-category, quantity, sales amount, and profit information.

**Attributes:**
- Order ID
- Category
- Sub-Category
- Quantity
- Amount
- Profit

### 3. Sales Target

Contains monthly sales targets for different product categories.

**Attributes:**
- Category
- Month of Order Date
- Target

These datasets support the analysis of sales trends, profitability, product performance, and actual sales compared with targets.

## 🛠️ Tools and Technologies

- **Microsoft Power BI Desktop** – Report development and data visualization.
- **DAX (Data Analysis Expressions)** – Calculated columns, measures, and time intelligence.
- **Power Query** – Data preparation and transformation completed in the previous assignment.
- **Data Modeling** – Relationships between orders, order details, and sales targets.
- **GitHub** – Project documentation and portfolio presentation.

## 🧮 DAX Calculations

### A. Calculated Columns

Calculated columns were created in the Order Details table to derive additional information for analysis.

#### 1. Category Type

Combines the Category and Sub-Category columns into a single field.

```dax
Category Type =
'Order Details'[Category] & " - " &
'Order Details'[Sub-Category]
```

**Purpose:** Makes it easier to identify and analyze products using a combined category and sub-category label.

#### 2. Revenue per Order

Calculates revenue using the Amount and Quantity columns, following the assignment requirement.

```dax
Revenue per Order =
'Order Details'[Amount] *
'Order Details'[Quantity]
```

**Purpose:** Creates a derived revenue value for each row in the Order Details table.

**Note:** This calculation follows the assignment instructions. If Amount already represents the total sales value for the row, multiplying it by Quantity may double-count quantity. The business meaning of Amount should be validated before interpreting this column as revenue.

#### 3. Sales Category

Categorizes each row as Above Average or Below Average based on its Amount compared with the average Amount in the Order Details table.

```dax
Sales Category =
IF(
    'Order Details'[Amount] >=
        CALCULATE(
            AVERAGE('Order Details'[Amount]),
            ALL('Order Details')
        ),
    "Above Average",
    "Below Average"
)
```

**Purpose:** Helps classify sales records relative to the overall average amount.

### B. Calculated Measures

Measures were developed to calculate business metrics dynamically within Power BI reports.

#### 1. Order Count

```dax
Order Count =
DISTINCTCOUNT('Order Details'[Order ID])
```

**Purpose:** Calculates the number of unique orders represented in the Order Details table. This avoids counting an order multiple times when it contains multiple product rows.

#### 2. Average Profit in Delhi

```dax
Average Profit in Delhi =
CALCULATE(
    AVERAGE('List of Orders'[Profit]),
    'List of Orders'[City] = "Delhi"
)
```

**Purpose:** Calculates the average profit for records associated with Delhi, respecting the applicable filter context.

#### 3. Year-to-Date (YTD) Sales

Assuming a properly configured Date table related to the order data:

```dax
YTD Sales =
TOTALYTD(
    [Total Sales],
    'Date'[Date]
)
```

The base measure can be defined as:

```dax
Total Sales =
SUM('Order Details'[Amount])
```

**Purpose:** Calculates cumulative sales from the beginning of the year through the selected date.

**Note:** The Date table should contain a continuous range of dates and be configured appropriately for time-intelligence calculations. If the assignment model does not include a Date table, create and relate one before using this YTD measure.

## 📈 Data Visualizations

The Power BI report includes the following visualizations to explore sales performance and business trends.

### 1. Sales Target Achievement by Category

**Visual:** Clustered Column Chart

Compares actual sales with sales targets for each product category.

**Business purpose:**
- Identify categories performing above or below their targets.
- Compare sales performance across product categories.
- Highlight categories that may require additional attention.

### 2. Maximum Profit Margin by Sub-Category

**Visual:** Donut Chart

Displays the maximum profit margin calculated for each product sub-category.

**Business purpose:**
- Compare maximum profit margin values across sub-categories.
- Identify product segments with relatively high profitability measures.

**Note:** Profit margin is normally calculated as Profit divided by Sales Amount. A suitable measure should be created and aggregated consistently before using maximum profit margin in this chart.

### 3. Monthly Sales Trend

**Visual:** Line Chart

Shows sales movement over time using monthly sales values.

**Business purpose:**
- Identify changes in sales across months.
- Recognize seasonal patterns and fluctuations.
- Monitor overall sales performance over time.

### 4. Profit and Quantity Comparison by Sub-Category

**Visual:** Scatter Chart

Compares profit and quantity sold for different product sub-categories.

**Business purpose:**
- Identify sub-categories with higher profits and sales quantities.
- Explore the relationship between quantity sold and profitability.
- Identify products that sell in high volumes but generate relatively low profits.

### 5. Total Sales Amount and Sales Target

**Visuals:** Card Visuals and Multi-Row Card

Displays the total sales amount, overall sales target, and minimum target for each segment represented in the report.

**Business purpose:**
- Present important business KPIs at a glance.
- Compare actual sales with planned targets.
- Identify segments with lower target values.

### 6. Sales Performance Matrix

**Visual:** Matrix

Displays actual sales and sales targets across product categories and months.

**Business purpose:**
- Compare monthly sales with targets.
- Identify high-performing and underperforming categories.
- Examine sales performance across different periods.

### 7. Geographic Sales Analysis

**Visual:** Map

Displays total sales by city to explore geographic sales patterns.

**Business purpose:**
- Identify cities contributing significantly to sales.
- Compare sales performance across locations.
- Highlight geographic areas that may offer growth opportunities.

### 8. Sales Distribution by Sub-Category

**Visual:** Treemap

Represents sales distribution across product sub-categories using differently sized rectangles.

**Business purpose:**
- Identify sub-categories contributing the largest share of sales.
- Compare the relative importance of product segments.
- Understand how sales are distributed across the product portfolio.

### 9. Order Count Analysis by State

**Visual:** Funnel Chart

Displays order counts across different states.

**Business purpose:**
- Compare order volumes between states.
- Identify states with relatively high or low order counts.
- Support geographic performance analysis.

**Note:** A funnel chart is generally designed for sequential stages. For independent state comparisons, a bar chart is often more suitable, but the funnel chart is retained to meet the assignment requirement.

## 🔍 Business Analysis and Key Questions

This project supports the exploration of several business questions:

- Which product categories achieve their sales targets?
- How do monthly sales change over time?
- Which sub-categories generate higher profits?
- How does quantity sold relate to profitability?
- Which cities and states contribute to sales performance?
- Which product sub-categories account for the largest share of sales?
- How does actual sales performance compare with monthly targets?
- What is the average profit for orders associated with Delhi?

The answers can help business stakeholders understand performance, identify areas requiring investigation, and make more informed decisions.

## 💡 Potential Business Recommendations

The following are possible recommendations to evaluate after reviewing the actual report results:

- **Improve target achievement:** Investigate categories that consistently fall below their sales targets and identify potential causes.
- **Optimize product performance:** Review low-profit sub-categories to understand their pricing, costs, and sales volumes.
- **Strengthen regional sales:** Explore opportunities in cities and states with lower order volumes or sales contributions.
- **Monitor monthly trends:** Use historical sales patterns to support inventory planning and sales forecasting.
- **Focus on profitable growth:** Evaluate sales volume alongside profit and profit margin instead of relying only on revenue.
- **Track KPIs consistently:** Monitor sales, targets, order counts, and profitability through an interactive dashboard.

These recommendations should be finalized only after validating the actual findings from the completed Power BI report.

## 📊 Dashboard Design

The report is designed to present business metrics and visual comparisons in a clear and interactive format.

The dashboard brings together:
- Sales and target comparison.
- Monthly sales trends.
- Profitability and quantity analysis.
- Category and sub-category performance.
- Geographic sales distribution.
- Order count analysis by state.
- KPI cards for quick performance monitoring.

Appropriate titles, labels, formatting, and consistent visual organization help users interpret the information efficiently.

## 📁 Project Structure

```text
E-Commerce-Sales-Analysis-PowerBI/
│
├── DAX & Data Visualization.pbix
├── README.md
│
└── Screenshots/
    ├── dashboard-overview.png
    ├── dax-calculated-columns.png
    ├── dax-measures.png
    ├── sales-target-by-category.png
    ├── monthly-sales-trend.png
    ├── profit-quantity-analysis.png
    ├── sales-performance-matrix.png
    └── geographic-sales-analysis.png
```

*The folder and screenshot names above are suggested examples. Add the files that you actually include in your repository.*

## 📦 Deliverables

- **Power BI report (.pbix):** Includes the existing data model, calculated columns, DAX measures, and visualizations.
- **Project documentation (README.md):** Explains the objectives, datasets, calculations, visualizations, and business applications.
- **PDF report:** Contains screenshots of DAX formulas, visualizations, dashboard layout, and brief explanations of each visual.

## 🎓 Skills Demonstrated

- DAX calculated columns and measures.
- Aggregation and filter context.
- Distinct order counting.
- Conditional logic using `IF` and `CALCULATE`.
- Time intelligence using `TOTALYTD`.
- Sales and profitability analysis.
- Target achievement analysis.
- Data visualization and dashboard development.
- Data modeling and relationship awareness.
- Business interpretation and analytical thinking.
- Technical documentation using GitHub Markdown.

## 🚀 Learning Outcomes

Through this project, I strengthened my understanding of how Power BI transforms business data into meaningful analytical reports. I practiced creating calculated columns and measures, applying DAX logic, comparing sales against targets, analyzing time-based trends, and selecting visualizations to communicate business performance.

This project is part of my ongoing journey toward becoming a **Data Analyst**, where I am building practical skills in Excel, Power BI, data analysis, and business intelligence.

## 👤 Author

**Aspiring Data Analyst**

I am developing my portfolio through hands-on projects focused on data cleaning, analysis, visualization, and business insights using tools such as Microsoft Excel and Power BI.

---

⭐ If you find this project useful, feel free to explore the repository and review the Power BI report and documentation.
