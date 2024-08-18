# northwind-product-recommendation
Northwind Product Recommendation System

Project Overview
This project implements a product recommendation system using the classic Northwind dataset. The aim is to provide personalized product suggestions based on customers' purchase history, demonstrating a practical application of data analysis, clustering techniques, and Python-SQL Server integration.

Features
Customer segmentation based on purchase behavior
Product recommendations tailored to specific customer clusters
Data extraction and manipulation using T-SQL in SQL Server
Data preprocessing, clustering, and recommendation logic implemented in Python
Visualization of clustering results and insights



Technologies Used
SQL Server: Data storage and querying
Python: Data processing, clustering (scikit-learn), and visualization (matplotlib, seaborn)
pandas: Data manipulation and analysis
pyodbc: Connecting Python to SQL Server


1-Install
required Python packages:
pip install -r requirements.txt
2-Set up the Northwind dataset in SQL Server.
3-Run the Python script to execute the analysis and generate recommendations.

Project Structure
data/: Contains SQL scripts and example datasets
notebooks/: Jupyter notebooks for step-by-step analysis
src/: Python scripts for data extraction, clustering, and recommendation logic



Results
The project provides insights into customer segments and recommends relevant products for each group, enhancing the decision-making process in a business scenario.

Future Improvements
Implement collaborative filtering for better recommendationsIntegrate with a web dashboard for real-time product suggestions.
