
# Nashville Housing Data Cleaning Project

## **Introduction**
This project focuses on cleaning and transforming the Nashville Housing dataset using SQL. The objective is to process and standardize the data, handle missing or inconsistent information, and prepare the dataset for further analysis or reporting. 

---

## **Project Workflow**

### **1. Standardizing Date Formats**
- Convert `SaleDate` to a standardized `Date` format.
- If the conversion fails:
  - Create a new column `SaleDateConverted` to store the cleaned date values.
  
**SQL Operations:**
- Use the `CONVERT(Date, SaleDate)` function.
- Update the table or add a new column if needed.

---

### **2. Populating Missing Property Addresses**
- Fill missing `PropertyAddress` values by matching `ParcelID` with other rows in the dataset.
- Use `ISNULL()` to select non-null values from duplicate rows.

**SQL Operations:**
- Join the table with itself on `ParcelID`.
- Update missing `PropertyAddress` values.

---

### **3. Breaking Out Address Components**
- Split `PropertyAddress` into `Address` and `City`.
- Use `SUBSTRING()` and `CHARINDEX()` for parsing.
- Similarly, split `OwnerAddress` into `OwnerSplitAddress`, `OwnerSplitCity`, and `OwnerSplitState`.

**SQL Operations:**
- Add new columns for each component.
- Update these columns using parsing functions (`SUBSTRING`, `PARSENAME`, etc.).

---

### **4. Updating "Sold As Vacant" Field**
- Standardize values in the `SoldAsVacant` field:
  - Convert `Y` to `Yes` and `N` to `No`.

**SQL Operations:**
- Use a `CASE` statement to update the column.

---

### **5. Removing Duplicates**
- Identify duplicates based on key columns (`ParcelID`, `PropertyAddress`, `SalePrice`, etc.).
- Use `ROW_NUMBER()` with `PARTITION BY` to flag duplicates.
- Delete rows where `ROW_NUMBER() > 1`.

**SQL Operations:**
- Use a Common Table Expression (CTE) to isolate duplicates.
- Delete the flagged rows.

---

### **6. Dropping Unused Columns**
- Remove columns that are no longer required, such as:
  - `OwnerAddress`, `TaxDistrict`, `PropertyAddress`, and `SaleDate`.

**SQL Operations:**
- Use the `ALTER TABLE` command with the `DROP COLUMN` clause.

---

### **7. Importing Data**
Two methods are provided for importing data:
1. **BULK INSERT:**
   - Load data from a `.csv` file.
   - Configure the SQL Server environment to support bulk operations.

2. **OPENROWSET:**
   - Read data directly from Excel or CSV files.
   - Requires enabling `Ad Hoc Distributed Queries`.

**SQL Operations:**
- Use `BULK INSERT` or `OPENROWSET` commands with appropriate configurations.

---

## **Tools Used**
- **SQL Server Management Studio (SSMS):** For executing queries and managing the database.
- **SQL Functions and Commands:**
  - `CONVERT`, `SUBSTRING`, `CHARINDEX`, `PARSENAME`
  - `CASE`, `ISNULL`, `ROW_NUMBER()`, `ALTER TABLE`

---

## **File Structure**
- **SQL Script:** Contains all the queries for cleaning and transforming the data.
- **Dataset:** Original Nashville Housing dataset in CSV format.
- **Documentation:**
  - This README file provides an overview of the project.

---

## **Key Learnings**
- Using SQL for data cleaning and transformation.
- Handling real-world edge cases like missing values, duplicates, and inconsistent formatting.
- Leveraging advanced SQL features like CTEs, window functions, and string parsing.

---

## **Future Enhancements**
- Automate the data cleaning process using stored procedures.
- Validate data integrity after each step using assertions or checks.
- Integrate the cleaned data with reporting tools for visualization.

---

## **How to Run the Project**
1. Load the `NashvilleHousing` dataset into your SQL Server.
2. Execute the queries in sequence to:
   - Standardize dates.
   - Populate missing data.
   - Clean up addresses and other fields.
   - Remove duplicates.
3. Use the transformed dataset for analysis or reporting.

--- 

## **Acknowledgments**
- The dataset and inspiration for this project are credited to the Nashville Housing data project.
- SQL Server documentation and tutorials for providing guidance on advanced functions.
