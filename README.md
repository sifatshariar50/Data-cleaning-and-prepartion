# E-Commerce Data
# ==========================================
# INCONSISTENT VALUES CHECKING & CLEANING
# ==========================================

# 1. Clean extra spaces in text columns
text_columns = ['Description', 'Country', 'StockCode']

for col in text_columns:
    df[col] = df[col].astype('string').str.strip()
    df[col] = df[col].str.replace(r'\s+', ' ', regex=True)

# 2. Standardize Country names
df['Country'] = df['Country'].str.title()

# 3. Check negative Quantity
negative_quantity = (df['Quantity'] < 0).sum()

# 4. Check zero and negative UnitPrice
zero_price = (df['UnitPrice'] == 0).sum()
negative_price = (df['UnitPrice'] < 0).sum()

# 5. Display unusual values before deciding what to do
print("========== INCONSISTENT VALUES REPORT ==========")

print("\nNegative Quantity:", negative_quantity)
print("Zero UnitPrice:", zero_price)
print("Negative UnitPrice:", negative_price)

print("\nCountry Names:")
print(df['Country'].unique())

# 6. Check missing values
print("\nMissing Values:")
print(df.isnull().sum())

# 7. Check duplicate rows
print("\nDuplicate Rows:", df.duplicated().sum())

# 8. Final dataset information
print("\nFinal Dataset Shape:", df.shape)

print("\nFinal Data Types:")
print(df.dtypes)

print("\nCleaning and checking completed!")
