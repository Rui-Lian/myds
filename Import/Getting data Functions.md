
[[list folder files and read by for loop]]

```r
# list of file names in raw1
# where the raw data are.
f_list <- list.files(path = "~/derm/raw1")

# Read files and combine them into one data frame
# Initialize an empty data frame
mydat <- data.frame()

# Loop through each file and read it
for (file in f_list) {
  # Read the Excel file
  file_path <- paste0("~/derm/raw1/", file)
  # Print to show the process.
  print(file_path)
  data <- read_excel(path = file_path)
  # Combine with the existing data frame
  mydat <- bind_rows(mydat, data)
}

# ANother way to do this reading
# List all Excel files in the directory
# excel_files <- list.files(path = dir_path, pattern = "\\.xlsx$", full.names = TRUE)
# Read all Excel files and combine into one data frame using lapply
# combined_data <- bind_rows(lapply(excel_files, read_excel))

# Remove the data file.
rm(data, f_list, file_path, file)
```

[[Read multiple files on one read without row binds]]

```r
sales_files <- c(
  "https://pos.it/r4ds-01-sales",
  "https://pos.it/r4ds-02-sales",
  "https://pos.it/r4ds-03-sales"
)
read_csv(sales_files, id = "file")
```

[[considerations of importing data]]

## type of delimitors

csv, tsv, semicolon, fwf...

[[column names tidy with janitor package]]

[[missing values and treatment of NA]]

[[data type and parsing]]


