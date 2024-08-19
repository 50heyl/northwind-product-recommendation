# northwind-product-recommendation
This project aims to implement a product recommendation system using the Northwind dataset. The recommendation model is based on customer segmentation through clustering techniques. The steps for implementing the solution are as follows:

### 1. **Importing the Northwind Database into SQL Server:**
   - If the database is not yet imported, load the `.sql` file into SQL Server using SSMS.
   - Once imported, you should see the Northwind database in SQL Server with tables like `Customers`, `Orders`, `Products`, etc.

### 2. **Connecting Python to SQL Server:**
   - Use `pyodbc` or `SQLAlchemy` to connect Python to SQL Server. For example:

   ```python
   import pyodbc

   conn = pyodbc.connect(
       'DRIVER={SQL Server};'
       'SERVER=your_server_name;'
       'DATABASE=Northwind;'
       'Trusted_Connection=yes;'
   )

   cursor = conn.cursor()
   ```

### 3. **Extracting Data from SQL Server:**
   - The first step is to retrieve customer, order, and product data from the database. For example:

   ```python
   query = """
   SELECT c.CustomerID, c.CompanyName, o.OrderID, od.ProductID, od.Quantity
   FROM Customers c
   JOIN Orders o ON c.CustomerID = o.CustomerID
   JOIN [Order Details] od ON o.OrderID = od.OrderID
   """

   cursor.execute(query)
   rows = cursor.fetchall()

   # Converting data to a DataFrame
   import pandas as pd
   df = pd.DataFrame([tuple(row) for row in rows], columns=['CustomerID', 'CompanyName', 'OrderID', 'ProductID', 'Quantity'])
   ```

### 4. **Data Analysis and Preprocessing:**
   - Review and clean the data to ensure it's ready for analysis using `pandas`:

   ```python
   # Checking the data
   print(df.head())
   # Handling missing values and cleaning data
   df.dropna(inplace=True)
   ```

### 5. **Customer Segmentation using Clustering:**
   - To build the recommendation system, customers are segmented based on their purchase patterns using K-Means clustering:

   ```python
   from sklearn.cluster import KMeans

   # Grouping customers by total quantity purchased
   customer_data = df.groupby('CustomerID').agg({'Quantity': 'sum'}).reset_index()

   

   kmeans = KMeans(n_clusters=3)  # Set the number of clusters
   customer_data['Cluster'] = kmeans.fit_predict(customer_data[['Quantity']])

   df=df.merge(customer_data[['CustomerID', 'Cluster']], on='CustomerID')

   import matplotlib.pyplot as plt
   %matplotlib inline

   plt.scatter(customer_data['CustomerID'], customer_data['Quantity'], c=customer_data['Cluster'], cmap='viridis')
   plt.xlabel('CustomerID')
   plt.ylabel('Quantity')
   plt.title('Customer Clusters')
   plt.show()
   ```

### 6. **Product Recommendation Based on Clusters:**
   - Products are recommended to each cluster based on what other customers in that cluster have frequently purchased:

   ```python
   # Assign the cluster lablels to the DataFrame
   customer_data['Cluster'] = kmeans.labels_

   # Most popular products for each cluster
   popular_products = df.groupby(['Cluster', 'ProductID']).agg({'Quantity': 'sum'}).reset_index()
   print(popular_products)
   ```
