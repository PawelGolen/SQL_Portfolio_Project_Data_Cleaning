# Nashville Housing Data Cleaning (SQL)

This repository contains a set of **SQL Server** queries used to clean and prepare the **Nashville Housing** dataset for analysis and visualization.

The script focuses on common data-cleaning tasks such as **date normalization**, **filling missing values**, **splitting columns**, **standardizing categorical values**, and **identifying duplicates**.

---

## ✅ What’s Included

The SQL script performs the following steps:

### 1) Standardize Date Format
- Converts `SaleDate` into a proper `DATE` type
- Adds a new column `SaleDateConverted` to store the cleaned date

### 2) Populate Missing Property Addresses
- For rows where `PropertyAddress` is `NULL`, it fills the value by joining on `ParcelID` and using another record with the same `ParcelID`

### 3) Split Property Address into Separate Columns
- Splits `PropertyAddress` into:
  - `PropertySplitAddress`
  - `PropertySplitCity`

### 4) Split Owner Address into Separate Columns
- Uses `PARSENAME` + `REPLACE` trick to split `OwnerAddress` into:
  - `OwnerSplitAddress`
  - `OwnerSplitCity`
  - `OwnerSplitState`

### 5) Normalize “Sold as Vacant” Values
- Converts:
  - `Y` → `Yes`
  - `N` → `No`
- Keeps other values unchanged

### 6) Identify Duplicates (CTE + ROW_NUMBER)
- Uses a CTE (`RowNumCTE`) with `ROW_NUMBER()` to find duplicate rows based on:
  - `ParcelID`, `PropertyAddress`, `SalePrice`, `SaleDate`, `LegalReference`

> Note: The script shows how to identify duplicates. Whether you delete them depends on your workflow and data governance rules.

### 7) Drop Unused Columns (Optional)
- Demonstrates removing columns such as:
  - `OwnerAddress`, `TaxDistrict`, `PropertyAddress`, `SaleDate`

> Recommended approach in production: avoid deleting raw columns in base tables; instead create **views** or **cleaned tables**.

---

## 🧰 Tech Stack

- **SQL Server / T-SQL**
- Window functions (`ROW_NUMBER()`)
- String functions (`SUBSTRING`, `CHARINDEX`, `PARSENAME`)
- DDL operations (`ALTER TABLE`, `DROP COLUMN`)

---

## ▶️ How to Run

1. Load the dataset into a SQL Server database (table: `PortfolioProject..NashvilleHousing`)
2. Run the SQL script step-by-step (recommended), especially:
   - `ALTER TABLE` statements (schema changes)
   - `DROP COLUMN` statements (destructive changes)

---

## ⚠️ Notes / Best Practices

- Always backup your dataset or work on a copy before running updates.
- Treat the original table as **raw** and create a **cleaned** version (table or view) for analytics.

---

## 📄 License

This project is available under the **MIT License**.
