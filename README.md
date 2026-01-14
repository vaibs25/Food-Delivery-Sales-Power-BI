# Food-Delivery-Sales-Power-BI

🍔 ZestyEats – Food Delivery Sales Analysis (Power BI)
📌 Project Overview

This project focuses on advanced data transformation, data modeling, and visualization in Power BI using a food delivery dataset.
The objective is to prepare raw operational data for analysis and then build KPI dashboards, analytical charts, and performance views that help evaluate sales, delivery efficiency, and customer behavior.

The project is completed in three phases:

Data Transformation

Data Modeling & Measure Creation

Visualization & Performance Analysis

🎯 Business Objectives

Categorize orders and customers for better segmentation

Create a unified fact table for analysis

Establish correct data relationships

Build reusable DAX measures

Analyze sales performance, delivery efficiency, and customer demographics

🛠️ Tools & Technologies

Power BI Desktop

Power Query – Data transformation

DAX – Measures & calculations

GitHub – Version control & documentation

🔄 Phase 1: Data Transformation (Power Query)
📄 Table: Order_details
➕ Conditional Column – Order Value Category

Column Name: Order Value Category

Order Value ≤ 500      → Low
Order Value ≤ 1000     → Medium
Else                   → High

➕ Calculated Column – Pickup Duration

Difference between:

Time Order Picked

Time Ordered

Data Type: Duration

📄 Table: User_details
➕ Conditional Column – Age Group

Column Name: Age group

Age ≤ 19   → Teen
Age ≤ 29   → Twenties
Age ≤ 39   → Thirties
Else       → Senior

🔗 Merging Tables (Final Fact Table Creation)

All merges are Left Joins, expanding only required columns:

Order_details ⟶ User_details

Join Key: Customer ID

Unselected: Customer ID

Result ⟶ Restaurant_details

Join Key: Restaurant ID

Unselected: Restaurant ID

Result ⟶ Delivery_details

Join Key: Order ID

Unselected: Order ID

Result ⟶ Delivery_person_details

Join Key: Delivery Person ID

Unselected: Delivery Person ID

✔ Final output is a single enriched Order_details table ready for modeling.

🧩 Phase 2: Data Modeling
📌 Fact Table

Order_details

🔗 Relationships
Many-to-One

Order_details ↔ User_details (Customer ID)

Order_details ↔ Restaurant_details (Restaurant ID)

Delivery_details ↔ Delivery_person_details (Delivery Person ID)

One-to-One

Order_details ↔ Delivery_details (Order ID)

📐 Core Measures (DAX)
🔢 Base Measures
Total Sales = SUM(Order_details[Order Value])

Average Order Value = AVERAGE(Order_details[Order Value])

Total Deliveries = DISTINCTCOUNT(Order_details[Order Id])

⏱️ On-Time Delivery %
On-time Delivery % =
DIVIDE(
    COUNTROWS(
        FILTER(Delivery_details, Delivery_details[Time Taken (Min)] <= 30)
    ),
    COUNTROWS(Delivery_details)
) * 100

📊 Phase 3: Advanced Measures for Analysis
Total Sales for Drinks =
CALCULATE(SUM(Order_details[Order Value]), Order_details[Type of Order] = "Drinks")

Total Sales for Snacks =
CALCULATE(SUM(Order_details[Order Value]), Order_details[Type of Order] = "Snack")

Total Sales All =
CALCULATE(SUM(Order_details[Order Value]), ALL(Order_details))

Sales Percentage =
DIVIDE(
    SUM(Order_details[Order Value]),
    CALCULATE(SUM(Order_details[Order Value]), ALL(Order_details))
)

Total Deliveries All =
CALCULATE(DISTINCTCOUNT(Order_details[Order Id]), ALL(Order_details))

Average Order Value All =
CALCULATE(AVERAGE(Order_details[Order Value]), ALL(Order_details))

On-time Delivery % All =
CALCULATE(
    DIVIDE(
        COUNTROWS(FILTER(Delivery_details, Delivery_details[Time Taken (Min)] <= 30)),
        COUNTROWS(Delivery_details)
    ) * 100,
    ALL(Delivery_details)
)

📊 Power BI Report Pages
📄 Page 1 – KPIs

Title: ZestyEats Performance View

KPI Cards

Total Sales All

Total Deliveries All

Average Order Value All

On-time Delivery % All

Total Sales for Drinks

Total Sales for Snacks

Total Sales

Total Deliveries

Average Order Value

On-time Delivery %

Donut Chart

Legend: Order Value Category

Values: Sales Percentage

Title: Sales Percentage by Order Value Category

Slicers (Dropdown)

Food Category

Type of Order

📄 Page 2 – Charts

Title: ZestyEats Performance View

Visuals

Stacked Column Chart

X-Axis: Food Category

Y-Axis: Count of Order ID

Legend: Order Value Category

Tooltip: Total Sales

Title: Order Value Distribution

Clustered Bar Chart

Y-Axis: Age Group

X-Axis: Count of Customer ID

Legend: Gender

Tooltip: Total Sales

Title: Customer Demographics

Pie Chart

Legend: Type of Order

Values: Total Sales

Title: Sales by Order Type

📄 Page 3 – Performance

Title: ZestyEats Performance View

Visuals

Line & Clustered Column Chart

X-Axis: Road Traffic Density

Column Y-Axis: Road Traffic Density

Line Y-Axis: Average Delivery Rating

Title: Delivery Performance

Scatter Plot

X-Axis: Delivery Person Age

Y-Axis: Average Time Taken

Legend: Type of Vehicle

Size: Vehicle Condition

Title: Delivery Person Efficiency

Treemap

Category: Type of Order

Details: Food Category

Values: Total Sales

Tooltips: Dine-in Available, Cuisine

Title: Restaurant Performance

📄 Page 4 – Matrix (Optional)
Matrix Visual

Rows: City → Age Group → Gender

Values:

Average Order Value

Order Count

Total Sales

🚀 Key Outcomes

Created a clean, analysis-ready fact table

Built scalable DAX measures

Delivered multi-page analytical dashboards

Enabled insights into sales mix, customer demographics, and delivery efficiency

📁 Project Files

📊 FoodDelivery_Sales_Charts.pbix – Power BI report

📄 README.md – Project documentation

🧠 Skills Demonstrated

Power Query Transformations

Data Modeling & Relationships

DAX Measures & KPIs

Dashboard & Performance Analysis

Business-Oriented BI Reporting
