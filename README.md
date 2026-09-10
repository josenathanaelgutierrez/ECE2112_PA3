# ECE 2112: Advanced Computer Programming and Algorithms
## Experiment 3: Python Data Analysis (Pandas)

### Repository Overview
This repository contains the Jupyter Notebook solution and corresponding dataset for **Experiment 3: Python Data Analysis (Pandas)**. The activity focuses on leveraging the powerful `pandas` library in Python to perform data manipulation, subsetting, and filtering on a provided CSV dataset (`cars.csv`). 

### Intended Learning Outcomes (Objectives)
At the end of this laboratory activity, students should be able to:
1. Load a CSV dataset into a Pandas DataFrame.
2. Select specific rows and columns utilizing both positional (`iloc`) and label-based (`loc`) indexing.
3. Filter records accurately using Boolean conditions on DataFrame columns.
4. Extract well-defined subsets of data while preserving the integrity of the original source dataset.

---

### Dataset Details
* **File:** `cars.csv`
* **Description:** A dataset containing various vehicle models alongside their corresponding engineering and performance metrics (e.g., mpg, cylinders, horsepower, weight, gears).

---

### Detailed Experiment Approach

#### Problem A: Positional and Label-Based Slicing
**Objective:** To extract a specific continuous chunk of rows and filter them to show only certain columns, combining positional and label-based indexing.

**Methodology:**
1. **Initial Inspection:** After loading the dataset using `pd.read_csv()`, the `.shape` attribute and `.columns` attribute are used to identify the dimensions and the exact column headers of the DataFrame.
2. **Positional Slicing (Rows):** The `.iloc[]` indexer is utilized to isolate rows 6 through 10. Since Python utilizes 0-based indexing, the first data row is index 0. Therefore, rows 6 to 10 correspond to index slice `[5:10]`. 
3. **Label-Based Slicing (Columns):** To extract only the `Model`, `mpg`, `cyl`, `hp`, and `gear` columns from the resulting subset, the `.loc[:, ['Col1', 'Col2', ...]]` method is applied. This ensures columns are selected by their explicit string labels rather than relying on column index numbers, increasing code readability and robustness.

#### Problem B: Model Lookup
**Objective:** To locate specific records based on their exact values within a column, avoiding the use of hard-coded row numbers.

**Methodology:**
1. **Toyota Corolla (Full Row):** Boolean masking is applied to the `Model` column (`cars['Model'] == 'Toyota Corolla'`). This generates a truth table used to filter the DataFrame, returning all variables/columns for this specific vehicle.
2. **Pontiac Firebird (Partial Row):** For the Pontiac Firebird, the condition `cars['Model'] == 'Pontiac Firebird'` is combined with the `.loc[]` accessor to dynamically fetch the row while simultaneously restricting the output to only the `Model`, `mpg`, `hp`, and `wt` columns. This prevents modifying the main dataset and retrieves exactly what is requested in a highly optimized single step.

#### Problem C: Multi-Model Subsetting
**Objective:** To extract records for multiple specific models (Datsun 710, Lotus Europa, and Ferrari Dino) and retain a specific subset of columns.

**Methodology:**
1. **Multi-condition Masking:** Instead of writing multiple chained `OR` statements, the pandas `.isin()` method is used on the `Model` column. A list of the target models `['Datsun 710', 'Lotus Europa', 'Ferrari Dino']` is passed as the argument.
2. **Simultaneous Column Selection:** The `.loc[]` indexer is deployed. The row condition is the `.isin()` mask, and the column condition is the required list `['Model', 'mpg', 'cyl', 'hp', 'gear']`.
3. **Validation:** The `.shape` of the resulting DataFrame (`selected_cars`) is printed to verify that it meets the strict structural requirement of exactly 3 rows and 5 columns.
