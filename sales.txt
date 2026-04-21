#1.importing libraries & loading data

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv("sales_data_sample.csv", encoding="latin1")
print(df.head())
df.columns = df.columns.str.strip()
print(df.info())

#2.Basic statistics in sales column(sum,mean,max,min)
print("\n=== BASIC SALES STATISTICS ===")

print("Total sales :", df["SALES"].sum())
print("Average :", df["SALES"].mean())
print("Maximum :", df["SALES"].max())
print("Minimum :",df["SALES"].min())

#3.Category-wise(Productline)sales
print("\n=== PRODUCT LINE SALES ===")

productline_sales = df.groupby("PRODUCTLINE")["SALES"].sum().sort_values(ascending=False)
print(productline_sales)

#4.Top-performing products(productcode)

print("\n=== TOP 5 PRODUCTS ===")

top_products = df.groupby("PRODUCTCODE")["SALES"].sum().sort_values(ascending=False).head(5)
print(top_products)

#5.Bar chart(Product Line)

plt.figure()
sns.barplot(x=productline_sales.index, y=productline_sales.values)
plt.title("Sales by Product Line")
plt.xlabel("Product Line")
plt.ylabel("sales")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

#6.Pie Chart(Product Line)

plt.figure()
productline_sales.plot(kind='pie')
plt.title("Sales Distribution by Prodcut Line")
plt.show()



