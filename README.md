# Customer Shopping Behavior Analysis — Python · SQL · Power BI

An end-to-end analytics project on 3,900 retail customer transactions: cleaning and feature engineering in Python, business analysis in SQL (PostgreSQL), an interactive Power BI dashboard, and a written report with recommendations.

**Business question:** *How can the company use consumer shopping data to identify trends, improve customer engagement, and optimize marketing and product strategies?*

## Tools
- **Python** (pandas, SQLAlchemy): data cleaning, feature engineering, loading into the database
- **PostgreSQL**: 10 business questions, using CTEs, window functions, and conditional aggregation
- **Power BI**: interactive dashboard
- **Report & deck**: findings and recommendations for stakeholders

## Dataset
`customer_shopping_behavior.csv`: 3,900 rows × 18 columns. It covers demographics (age, gender, location), purchase details (item, category, amount, size, color, season), and behavior (review rating, subscription, shipping type, discount, previous purchases, payment method, purchase frequency).

## Workflow
1. **Data preparation** ([notebook](Customer_Shopping_Behavior_Analysis.ipynb))
   - Filled 37 missing review ratings with the median rating of each category
   - Standardized column names to snake_case
   - Engineered `age_group` (age quartiles) and `purchase_frequency_days`
   - Dropped `promo_code_used`, which always matches `discount_applied`
   - Loaded the cleaned data into PostgreSQL. The connection code for MySQL and SQL Server is included too.
2. **SQL analysis** ([queries](customer_behavior_sql_queries.sql)): revenue by gender and age group, discount behavior, product ratings, shipping, subscriptions, customer segmentation, and the top products per category
3. **Dashboard** (`customer_behavior_dashboard.pbix`)
4. **Report & presentation**: `Customer Shopping Behavior Analysis.pdf`, `Customer-Shopping-Behavior-Analysis.pptx`

## Key findings
- **Revenue by gender:** male customers generated $157.9K vs. $75.2K for female customers, about 68% of revenue. This partly reflects the customer mix: 2,652 of the 3,900 customers are male.
- **Data caveat:** every discounted purchase in the dataset was made by a male customer. Discount effects and gender effects can't be separated, so conclusions about either should be treated with caution.
- **Loyalty:** 80% of customers are *Loyal* (more than 10 previous purchases), 18% are *Returning*, and only 2% are *New*.
- **Subscriptions:** subscribers don't spend more per purchase ($59.49 vs. $59.87). Repeat buyers (more than 5 previous purchases) subscribe at a slightly higher rate than everyone else (27.6% vs. 22.4%).
- **Shipping:** Express orders average a little more than Standard orders ($60.48 vs. $58.46).
- **Products:** Gloves, Sandals, and Boots have the highest average ratings, but every product falls within a narrow 3.6–3.9 range. Hats and Sneakers are discounted most often, at about 50% of purchases.
- **Age:** revenue is spread evenly across age groups (24–27% each). Young Adults contribute the most.

## How to run
1. Create a PostgreSQL database named `customer_behavior`.
2. Set your database password as an environment variable:
   ```bash
   export DB_PASSWORD='your_password'
   ```
3. Run the notebook to clean the data and load it into the `customer` table.
4. Run `customer_behavior_sql_queries.sql`. The queries are written for PostgreSQL. The header of the file explains how to adapt them for MySQL or SQL Server.
5. Open `customer_behavior_dashboard.pbix` in Power BI Desktop and point it at your database.

## Author
**Vikhyat Koppal**: [GitHub](https://github.com/VikhyatKoppalgithub)

## Acknowledgements
This project builds on the [customer trends portfolio project](https://github.com/amlanmohanty1/customer-trends-data-analysis-SQL-Python-PowerBI) by Amlan Mohanty (MIT License).
