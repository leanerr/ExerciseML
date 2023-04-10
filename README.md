# Exercise 2 - Product Sales


#1. 
The orders_items table is used to represent the items that were included in each order in the orders table. It has a many-to-many relationship with the products table, since each order can contain multiple products, and each product can be included in multiple orders. The quantity column represents the number of units of a given product that were included in a given order.


#2.
#SQL query to find the average order cost per country 



```
SELECT c.country, AVG(o.order_cost) AS avg_order_cost
FROM customers c
JOIN orders o ON c.id = o.id_customer
GROUP BY c.country;
```

This query joins the customers and orders tables on the customer ID, and groups the results by country. The AVG function is used to calculate the average order cost for each country.


#3. SQL query to find the name of the highest price product sold to an Italian customer:



```
SELECT p.name
FROM products p
JOIN orders_items oi ON p.id = oi.id_product
JOIN orders o ON oi.id_order = o.id
JOIN customers c ON o.id_customer = c.id
WHERE c.country = 'Italy'
ORDER BY p.price DESC
LIMIT 1;
```

This query joins the products, orders_items, orders, and customers tables to find the highest price product sold to an Italian customer. It first filters the customers table to only include customers from Italy, then joins the orders_items table to the products table to get the name and price of each product sold. Finally, it sorts the results by price in descending order, and uses LIMIT 1 to only return the highest-priced product.



#**4**. 

To optimize the orders table for a high volume of queries, we could consider using indexing. For example, you could create an index on the id_customer column in the orders table, which would make it faster to look up all orders for a given customer. we could also create indexes on other frequently queried columns, such as order_cost or order_date.

there are a few other techniques that can be used to optimize the orders table for a high volume of queries:
Partitioning: This involves splitting the orders table into multiple smaller tables based on a chosen partitioning key (such as date, customer ID, or order status). This can help reduce query times by allowing queries to be executed on smaller subsets of the data.

Denormalization: This involves duplicating data across tables in order to reduce the need for joins. For example, you could denormalize the orders table by including the customer name and country in each row, rather than requiring a join with the customers table for each query.

Caching: This involves storing the results of frequently executed queries in memory or on disk, so that they can be served quickly without needing to hit the database.

#**5**.

if the amount of data is too big to run these queries efficiently, we would need to consider using a distributed database system or a data warehouse. These types of systems are designed to handle large volumes of data and can parallelize queries across multiple nodes to improve performance. we may also need to consider using more specialized database technologies, such as columnar databases or NoSQL databases, depending on the specific requirements of your queries.

When dealing with very large amounts of data, traditional relational databases may not be sufficient to handle the volume and complexity of the data. In this case, there are a few options for managing the data:
Distributed databases: These are databases that are designed to scale horizontally across multiple nodes, allowing them to handle large volumes of data and traffic. Examples of distributed databases include Apache Cassandra and Amazon DynamoDB.

Data warehouses: These are specialized databases that are designed to handle large volumes of structured data, typically for business intelligence or reporting purposes. They often include features such as columnar storage, parallel processing, and advanced query optimization. Examples of data warehouses include Amazon Redshift and Google BigQuery.

NoSQL databases: These are databases that are designed to handle unstructured or semi-structured data, such as JSON or XML documents. They are often used in applications such as web and mobile apps, where data is generated and consumed in a highly distributed and heterogeneous fashion. Examples of NoSQL databases include MongoDB and Apache CouchDB.




# Exercise 3 - Machine Translation





### **1**.
Designing a data pipeline for a Machine Translation system involves several key steps:
Data collection: This involves sourcing parallel data (i.e. text in two or more languages) that can be used to train and evaluate the machine translation model. Sources of parallel data include publicly available corpora, websites with multilingual content, and human translators.

Data preprocessing: This involves cleaning and formatting the raw data to make it suitable for training the machine translation model. This includes tasks such as tokenization, sentence splitting, and language identification.

Model training: This involves training the machine translation model using the preprocessed parallel data. Popular machine translation models include sequence-to-sequence models, transformer models, and neural machine translation models.

Model evaluation: This involves evaluating the performance of the trained machine translation model using metrics such as BLEU, METEOR, and TER. This helps identify areas where the model may be making errors or performing poorly, and can inform decisions about further training or model tuning.

Model deployment: This involves deploying the trained machine translation model in a production environment, where it can be used to translate new input text.

Some of the main challenges involved in designing a data pipeline for a Machine Translation system include:

Sourcing high-quality parallel data in the desired languages
Preprocessing the data to ensure that it is suitable for training the model
Choosing an appropriate machine translation model architecture and tuning its parameters
Ensuring that the deployed system is fast and reliable, and that it can handle the volume and variety of input text that it may encounter in production.

---

### **2**.
Collecting new and good quality data from the web for machine translation training can be a challenging task. Some strategies that can be used include:
Scraping multilingual websites: Websites that contain content in multiple languages can be scraped to collect parallel data for machine translation training. This can be done using tools such as BeautifulSoup or Scrapy.

Collaborating with human translators: Professional translators can be engaged to create new parallel data specifically for machine translation training. This can be done through crowdsourcing platforms such as Amazon Mechanical Turk or specialized translation agencies.

Using existing translation memories: Translation memories are databases of previously translated texts that can be leveraged for machine translation training. Many translation agencies and language service providers have translation memories that can be licensed or accessed for free.

Regardless of the approach used, it's important to ensure that the collected data is of high quality and representative of the types of input text that the machine translation system will encounter in production.

---

### **3**.
To monitor the quality of a machine translation system using post-editing by professional translators, the following steps can be taken:
Collect a sample of output translations generated by the machine translation system
Have professional translators review and edit the output translations to improve their quality
Compare the post-edited translations to the original input text, as well as to the output generated by the machine translation system, to identify areas where the system is making errors or producing poor-quality translations
Use this feedback to refine and improve the machine translation model and its training data, with the goal of reducing the need for post-editing in the future.


---



