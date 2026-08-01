<h1 align="center"><b>🍕 FOOD SALES ANALYSIS</b></h1>
<p align="center">
  <img width="703" height="577" alt="image" src="https://github.com/user-attachments/assets/aace593c-1580-4322-888e-c8d27877f5be" />
</p>




# 🍕 Business Problem

Managing a large volume of sales data can be challenging for a growing pizza business. With **over 50,000 sales records**, the company requires a **robust and scalable data analytics solution** to transform raw transactional data into meaningful business insights.

The objective of this project is to analyze sales data to uncover key trends, customer purchasing behavior, menu performance, and overall business performance. By leveraging **SQL for data cleaning, transformation, and analysis** along with **Power BI for interactive visualization**, the project enables the business to monitor critical Key Performance Indicators (KPIs) such as revenue, order volume, product performance, and customer preferences.

The dashboard provides insights into:

* 📈 Daily and Monthly Sales Trends
* 🍕 Best & Worst Selling Pizzas
* 📊 Sales Distribution by Pizza Category and Size
* 💰 Revenue Performance
* 🛒 Customer Ordering Patterns
* 📦 Order Volume Analysis

These insights empower stakeholders to make **data-driven decisions**, optimize inventory and staffing, improve menu offerings, enhance customer satisfaction, and ultimately increase overall business profitability.

# 🚀 Solution Plan

To transform the pizza company's raw sales data into meaningful business insights, this project follows a structured data analytics workflow using **SQL** and **Power BI**.

The process begins with **data cleaning and preprocessing**, where the CSV dataset is prepared by handling inconsistencies, ensuring data accuracy, and transforming the data into a suitable format for analysis. Once the dataset is cleaned, **SQL** is used to perform data exploration and analysis, enabling the extraction of valuable business metrics such as total revenue, average order value, total orders, total pizzas sold, and the best- and worst-performing menu items.

After the analytical phase, the processed data is imported into **Power BI** to create an interactive and visually appealing dashboard. Various charts, graphs, and KPI cards are designed to present insights in a clear and intuitive manner, allowing stakeholders to quickly understand business performance and identify trends.

The dashboard provides interactive analysis of:

* 📈 Daily and Monthly Sales Trends
* 💰 Revenue and Order Performance
* 🍕 Sales by Pizza Category and Size
* 🏆 Top & Bottom Selling Pizzas
* 📊 Customer Ordering Patterns
* 📦 Key Business Performance Indicators (KPIs)

By combining the analytical capabilities of SQL with the visualization power of Power BI, the project delivers a comprehensive business intelligence solution that enables stakeholders to monitor performance, identify growth opportunities, optimize operations, and make informed, data-driven decisions to improve overall profitability.

# Execution

## Questions Answered from the Dataset

### 1) What are the Key Performance Indicators obtained from the Dataset?

#### Total Revenue

```sql
SELECT SUM(total_price) AS Total_Revenue
FROM pizza_sales;
```
<img width="446" height="217" alt="image" src="https://github.com/user-attachments/assets/77cf8884-b910-459f-87f9-ceca5f9becb2" />

This metric provides a clear measure of the overall financial performance of pizza sales. It indicates the total amount of revenue generated from all pizza orders during a specific period, helping evaluate the business's overall revenue performance and profitability.

### 💳 Average Order Value

```sql
SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_Order_Value
FROM pizza_sales;
```
<img width="478" height="217" alt="image" src="https://github.com/user-attachments/assets/2aee149a-9aaf-4f85-9e55-fe8889ab4c9e" />



**Insight**

Average Order Value (AOV) measures the average amount spent by a customer per order. This KPI helps analyze customer spending behavior and evaluate the effectiveness of pricing and marketing strategies. A higher average order value indicates that customers are spending more per transaction, contributing to increased revenue and overall business profitability.

### 🍕 Total Pizzas Sold

```sql id="06x9v9"
SELECT SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales;
```

<img width="480" height="230" alt="image" src="https://github.com/user-attachments/assets/631fd5ca-b450-43a6-9a47-2a1ae0ec6957" />

**Insight**

Total Pizzas Sold is a key performance indicator that measures the overall demand for pizza products. It provides valuable insights into customer purchasing patterns and supports effective inventory management, production planning, and demand forecasting. Monitoring this metric helps businesses ensure product availability, optimize operations, and meet customer demand efficiently.

### 📦 Total Orders

```sql id="d8nvh2"
SELECT COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales;
```
<img width="479" height="198" alt="image" src="https://github.com/user-attachments/assets/16a51acd-4c1b-4678-8a3d-3dd8c385b741" />

**Insight**

Total Orders represents the total number of unique customer transactions processed during the selected period. This KPI helps evaluate overall sales performance, analyze customer purchasing trends, and measure business growth. Monitoring total orders also supports operational planning, resource allocation, and performance assessment.

### 📈 Average Pizzas per Order

```sql id="rlx1zc"
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) /
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
AS Avg_Pizzas_Per_Order
FROM pizza_sales;
```
<img width="511" height="245" alt="image" src="https://github.com/user-attachments/assets/f2f25ad3-c979-4c46-aeae-06a49c4df0d2" />

**Insight**

Average Pizzas per Order measures the average number of pizzas purchased in each customer transaction. This KPI provides valuable insights into customer ordering behavior and purchasing patterns. A higher average indicates that customers tend to buy multiple pizzas per order, highlighting opportunities for upselling, combo offers, and identifying popular menu items that contribute to increased sales.

### 📅 Daily Trend for Total Orders

```sql id="hsj3l7"
SELECT DATENAME(DW, order_date) AS order_day,
       COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY DATENAME(DW, order_date);
```
<img width="570" height="509" alt="image" src="https://github.com/user-attachments/assets/461b5dcc-15f7-4706-b90e-31fa1b54ab43" />

**Insight**

The Daily Trend for Total Orders provides a clear view of customer ordering patterns throughout the week. By analyzing daily order volumes, businesses can identify peak and low-demand days, understand customer purchasing behavior, and allocate resources more effectively. These insights support better inventory management, staffing decisions, and operational planning to ensure efficient service during high-demand periods.

### 📅 Monthly Trend for Orders

```sql id="3bxygv"
SELECT DATENAME(MONTH, order_date) AS Month_Name,
       COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY DATENAME(MONTH, order_date);
```
<img width="497" height="693" alt="image" src="https://github.com/user-attachments/assets/09790789-1ae8-4215-8e92-732c8ee96b91" />

**Insight**

### 🍕 Percentage of Sales by Pizza Category

```sql id="o5pvw9"
SELECT pizza_category,
       CAST(SUM(total_price) AS DECIMAL(10,2)) AS Total_Revenue,
       CAST(SUM(total_price) * 100 /
       (SELECT SUM(total_price) FROM pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category;
```
<img width="921" height="429" alt="image" src="https://github.com/user-attachments/assets/9711a9a7-4b80-4166-a233-f7e14e417d6c" />


**Insight**

The Percentage of Sales by Pizza Category illustrates the revenue contribution of each pizza category to total sales. This analysis helps identify the most popular categories, understand customer preferences, and evaluate each category's impact on overall revenue. These insights support data-driven decisions for menu optimization, inventory planning, and targeted marketing strategies to enhance customer satisfaction and maximize profitability.

The Monthly Trend for Orders provides an overview of customer order activity across different months. Analyzing monthly order volumes helps identify seasonal trends, peak sales periods, and slower business months. These insights enable businesses to optimize inventory management, production planning, staffing, and promotional strategies, ensuring efficient operations while maximizing revenue during high-demand periods.

### 📏 Percentage of Sales by Pizza Size

```sql id="f4sxza"
SELECT pizza_size,
       CAST(SUM(total_price) AS DECIMAL(10,2)) AS Total_Revenue,
       CAST(SUM(total_price) * 100 /
       (SELECT SUM(total_price) FROM pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size;
```
<img width="849" height="506" alt="image" src="https://github.com/user-attachments/assets/44044f00-4ce5-4643-a158-08539760b402" />

**Insight**

This analysis shows the percentage contribution of each pizza size to the total sales revenue. It provides valuable insights into customer preferences for different pizza sizes and highlights which sizes generate the highest sales. These findings help businesses optimize inventory management, refine menu offerings, and develop pricing and promotional strategies to better meet customer demand and maximize revenue.

### 🍕 Total Pizzas Sold by Pizza Category

```sql id="c3k9ma"
SELECT pizza_category,
       SUM(quantity) AS Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC;
```
<img width="869" height="416" alt="image" src="https://github.com/user-attachments/assets/0037b1b9-e31c-4731-92fa-52d9c1d17897" />


**Insight**

This analysis displays the total number of pizzas sold for each pizza category during the selected month. It enables a comparison of sales performance across different categories, helping identify the most and least popular pizza types. These insights assist businesses in optimizing menu offerings, improving inventory management, and developing targeted marketing strategies to enhance customer satisfaction and drive higher sales.

### 🏆 Top 5 Pizzas by Revenue

```sql
SELECT TOP 5 pizza_name,
       SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC;
```

<img width="797" height="369" alt="image" src="https://github.com/user-attachments/assets/766ce813-83c1-49e2-98fe-a71577f680f4" />



**Insight**

This analysis identifies the top five pizzas that generated the highest revenue. It highlights the best-performing menu items, helping the business understand customer preferences and purchasing trends. These insights support targeted promotions, menu optimization, and strategies to maximize revenue.

---

### 📉 Bottom 5 Pizzas by Revenue

```sql
SELECT TOP 5 pizza_name,
       SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC;

<img width="878" height="339" alt="image" src="https://github.com/user-attachments/assets/f15cb2c1-7979-478b-867c-c4ec402d9f54" />


**Insight**

This analysis identifies the five pizzas that generated the lowest revenue. It helps uncover underperforming menu items and provides valuable insights for making strategic decisions, such as revising the menu, adjusting pricing, or introducing promotional campaigns to improve sales.

---

### 🍕 Top 5 Pizzas by Quantity Sold

```sql
SELECT TOP 5 pizza_name,
       SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC;
```

<img width="1074" height="461" alt="image" src="https://github.com/user-attachments/assets/4ed96bc1-8caa-4396-9f9b-cef168d8659e" />


**Insight**

This analysis identifies the five pizzas with the highest quantity sold, revealing the most popular pizza varieties among customers. Understanding these preferences enables businesses to optimize inventory, improve menu offerings, and design targeted marketing campaigns to increase sales.

---

### 📉 Bottom 5 Pizzas by Quantity Sold

```sql
SELECT TOP 5 pizza_name,
       SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC;
```

<img width="1008" height="446" alt="image" src="https://github.com/user-attachments/assets/dc0ef18c-1fab-4fd4-b7d6-b09d75248985" />


**Insight**

This analysis identifies the five pizzas with the lowest quantity sold, highlighting less popular or underperforming menu items. These insights help businesses improve inventory management, refine marketing strategies, and optimize the menu to minimize waste and maximize profitability.

---

### 🛒 Top 5 Pizzas by Total Orders

```sql
SELECT TOP 5 pizza_name,
       COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC;
```

<img width="797" height="412" alt="image" src="https://github.com/user-attachments/assets/6c03507f-6b53-4391-a6cd-f92b6224e820" />


**Insight**

This analysis identifies the five pizzas with the highest number of customer orders. It provides valuable insights into customer preferences and ordering behavior, enabling businesses to tailor marketing campaigns, optimize menu offerings, and ensure sufficient inventory for high-demand products.

---

### 📉 Bottom 5 Pizzas by Total Orders

```sql
SELECT TOP 5 pizza_name,
       COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC;
```

<img width="754" height="327" alt="image" src="https://github.com/user-attachments/assets/f5781d32-6cda-4849-bd55-1f53157fe216" />


**Insight**

This analysis identifies the five pizzas with the lowest number of customer orders, revealing less popular menu items. Understanding these trends helps businesses make informed decisions regarding menu optimization, promotional strategies, and inventory planning to improve customer satisfaction and overall sales performance.

# 🎯 Conclusion

This project successfully transformed raw pizza sales data into meaningful business insights using **SQL** and **Power BI**. Through comprehensive data analysis, key trends in customer behavior, sales performance, and menu popularity were identified, enabling a deeper understanding of the business.

The analysis revealed valuable insights such as peak and low-demand periods through daily and monthly sales trends, helping optimize staffing, inventory management, and operational planning. Additionally, analyzing sales distribution across pizza categories and sizes provided a clear understanding of customer preferences, supporting more effective menu optimization and targeted marketing strategies.

Furthermore, key performance indicators—including Total Revenue, Average Order Value, Total Orders, Total Pizzas Sold, and Average Pizzas per Order—offered a comprehensive overview of business performance. Identifying the top and bottom-performing pizzas based on revenue, quantity sold, and total orders also enabled informed decision-making regarding pricing, promotions, and product offerings.

Overall, this project demonstrates how data analytics and business intelligence can empower organizations to make data-driven decisions, improve operational efficiency, enhance customer satisfaction, and drive sustainable business growth in the competitive food service industry.

