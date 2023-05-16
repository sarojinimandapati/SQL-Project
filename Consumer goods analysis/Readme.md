# Domain:  Consumer Goods | Function: Executive Management
### Atliq Hardwares (imaginary company) is one of the leading computer hardware producers in India and well expanded in other countries too.
* However, the management noticed that they do not get enough insights to make quick and smart data-informed decisions. 
* They want to expand their data analytics team by adding several junior data analysts.
* Tony Sharma, their data analytics director wanted to hire someone who is good at both tech and soft skills. Hence, he decided to conduct a SQL challenge which will help him understand both the skills.    

# DATA
### The file provides a comprehensive overview of the tables found in the 'gdb023' (atliq_hardware_db) database. It includes information for six main tables:

1. dim_customer: contains customer-related data
2. dim_product: contains product-related data
3. fact_gross_price: contains gross price information for each product
4. fact_manufacturing_cost: contains the cost incurred in the production of each product
5. fact_pre_invoice_deductions: contains pre-invoice deductions information for each product
6. fact_sales_monthly: contains monthly sales data for each product.

#### Column Description for dim_customer table:
1. customer_code: The 'customer_code' column features unique identification codes for every customer in the dataset. These codes can be used to track a customer's saleshistory, demographic information, and other relevant details. For example, the codes could look like '70002017', '90005160', and '80007195' respectively.

2. customer: The 'customer' column lists the names of customers, for example 'Atliq Exclusive', 'Flipkart', and 'Surface Stores' etc.

3. platform: The 'platform' column identifies the means by which a company's products or services are sold. "Brick & Mortar" represents the physical store/location, and "E-Commerce" represents online platforms.

4. channel: The 'channel' column reflects the distribution methods used to sell a product. These methods include "Retailers", "Direct", and "Distributors". Retailers refer to physical or online stores that sell products to consumers. Direct sales refer to sales made directly to consumers through a company's website or other direct means, and distributors refer to intermediaries or middlemen between the manufacturer and retailer or end consumers.

5. market: The 'market' column lists the countries in which the customer is located.

6. region: The 'region' column categorizes countries according to their geographic location, including "APAC" (Asia Pacific), "EU" (Europe), "NA" (North America), and 	"LATAM" (Latin America).

7. sub_zone: "The 'sub_zone' column further breaks down the regions into sub-regions, such as "India", "ROA" (Rest of Asia), "ANZ" (Australia and New Zealand), "SE" 	Southeast Asia), "NE" (Northeast Asia), "NA" (North America), and "LATAM" (Latin America)."


#### Column Description for dim_product table:
1. product_code: The 'product_code' column features unique identification codes for each product, serving as a means to track and distinguish individual products within a 		database or system.

2. division: The 'division' column categorizes products into groups such as "P & A" (Peripherals and Accessories), "N & S" (Network and Storage) and "PC" (Personal 				 Computer).

3. segment: The 'segment' column categorizes products further within the division, such as "Peripherals" (keyboard, mouse, monitor, etc.), "Accessories" (cases, cooling solutions, power supplies), "Notebook" (laptops), "Desktop" (desktops, all-in-one PCs, etc), "Storage" (hard disks, SSDs, external storage), and "Networking" (routers, switches, modems, etc.).

4. category: The 'category' column classifies products into specific subcategories within the segment.

5. product: The 'product' column lists the names of individual products, corresponding to the unique identification codes found in the 'product_code' column.

6. variant: The "variant" column classifies products according to their features, prices, and other characteristics. The column includes variants such as "Standard", "Plus", "Premium" that represent different versions of the same product.

#### Column Description for fact_gross_price table:
1. product_code: The 'product_code' column features unique identification codes for each product.

2. fiscal_year: The 'fiscal_year' column contains the fiscal period in which the product sale was recorded. A fiscal year is a 12-month period that is used for accounting purposes and often differs from the calendar year. For Atliq Hardware, the fiscal year starts in September. The data available in this column covers the 	fiscal years 2020 and 2021.

3. gross_price: The 'gross_price' column holds the initial price of a product, prior to any reductions or taxes. It is the original selling price of the product.

#### Column Description for fact_manufacturing_cost:
1. product_code: The 'product_code' column features unique identification codes for each product

2. cost_year: The "cost_year" column contains the fiscal year in which the product was manufactured.

3. manufacturing_cost: The "manufacturing_cost" column contains the total cost incurred for the production of a product. This cost includes direct costs like
raw materials, labor, and overhead expenses that are directly associated with the production process.

#### Column Description for fact_pre_invoice_deductions:
1. customer_code: The 'customer_code' column features unique identification codes for every customer in the dataset. These codes can be used to track a customer's sales history, demographic information, and other relevant details. For example, the codes could look like '70002017', '90005160', and '80007195' respectively.

2. fiscal_year: The "fiscal_year" column holds the fiscal period when the sale of a product occurred.

3. pre_invoice_discount_pct: The "pre_invoice_discount_pct" column contains the percentage of pre-invoice deductions for each product. Pre-invoice deductions are 
discounts that are applied to the gross price of a product before the invoice is generated, and typically applied to large orders or long-term contracts.

#### Column Description for fact_sales_monthly:
1. date: The "date" column contains the date when a product was sold, in a monthly format for 2020 and 2021 fiscal years. This information can be used
to understand the sales performance of products over time.

2. product_code: The "product_code" column contains a unique identification code for each product. This code is used to track and differentiate individual 
products within a database or system.

3. customer_code: The 'customer_code' column features unique identification codes for every customer in the dataset. These codes can be used to track a customer's sales history, demographic information, and other relevant details. For example, the codes could look like '70002017', '90005160', and '80007195' respectively.

4. sold_quantity: The "sold_quantity" column contains the number of units of a product that were sold. This information can be used to understand the sales volume of products and to compare the sales volume of different products or variants.

5. fiscal_year: The "fiscal_year" column holds the fiscal period when the sale of a product occurred.

# Requests

#### 1. Provide the list of markets in which customer "Atliq Exclusive" operates its business in the APAC region.

-> select  market from dim_customer where customer="Atliq Exclusive" and region="APAC";


<img width="120" alt="Screenshot 2023-05-16 194520" src="https://github.com/sarojinimandapati/SQL-Projects/assets/124454596/d163ff31-8218-4fe2-bfca-6a27272bb203">  

The above result set is the list of markets where Atliq is exclusive in the APAC region.

#### 2. What is the percentage of unique product increase in 2021 vs. 2020? The final output contains these fields,unique_products_2020unique_products_2021 percentage_chg.

select prev.A as unique_products_2020,next.B as unique_products_2021,round(((B-A)/A)*100,1) as percentage_chng 
from (
(select count(distinct product_code) A from fact_gross_price where fiscal_year=2020) as prev,
(select count(distinct product_code) B from fact_gross_price where fiscal_year=2021) as next) ;

<img width="295" alt="image" src="https://github.com/sarojinimandapati/SQL-Projects/assets/124454596/0cc3c4db-8f91-4080-b365-4c46e4586c45">


