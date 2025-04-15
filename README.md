### 📘 `read_data_dict()`

This function exports the **full REDCap Data Dictionary** for a specified database and **matches it to a given dataset**, producing a cleaned and tailored data dictionary. It handles standard variables and properly expands checkbox variables into their individual components.

---

#### 🧠 Purpose

- Extract the REDCap data dictionary using an API token.
- Match it to the dataset’s variables.
- Format and clean the dictionary for use in documentation or codebooks.
- Handle special cases for checkboxes, expanding them into individual entries.

---

#### ⚙️ Usage

```r
read_data_dict(data, token)
```

- `data`: A data frame containing REDCap-exported data.
- `token`: The API token for the REDCap project.

---

#### ✅ Example

```r
read_data_dict(df, contact_token)
```

---

#### 🔍 Function Details

1. **Export REDCap Metadata**
   - Uses an API call to download the metadata in CSV format using the provided token.

2. **Match to Dataset**
   - Filters and keeps only the metadata fields that appear in the dataset.
   - Cleans HTML tags and standardizes common field types.

3. **Response Options Cleanup**
   - `yesno`, `text`, and `notes` types are replaced with standard human-readable descriptions.
   - Labels for known fields (e.g., `global_id`, `nacc_id`) are adjusted.

4. **Checkbox Handling**
   - REDCap exports checkboxes as multiple variables (e.g., `race___1`, `race___2`, etc.).
   - These are not listed separately in the metadata.
   - This function reconstructs the checkbox options into individual entries.
   - Adds readable labels like `Race: Black`, `Race: White`, etc.

5. **Final Dictionary Assembly**
   - Combines the expanded checkbox metadata with the rest.
   - Reorders variables to ensure consistency with the original data.
   - Stores the result in a global variable: `data_dict`.

---

#### 📦 Output

- Creates a cleaned and expanded data dictionary stored in the global variable `data_dict`.
- Includes:
  - All variables from the original dataset.
  - Expanded checkbox variables with individual labels.
  - Useful for automated documentation or review.

---

> 🔁 **Note:** This function modifies a global variable (`data_dict`). If used in a package or modular script, consider returning the data dictionary instead of relying on a global assignment.
