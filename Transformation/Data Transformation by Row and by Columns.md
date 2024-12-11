
cmd+shift+m to insert pipe


## Row operations

#filter #arrange #distinct #count

## Column operations

#mutate #select #rename #relocate

### mutate

.before, .after, .keep

### select
 column_name : column_name

[[select helpers]]


[[make names]]



Relocate column, this is better than select and the column sequence. 

```r
# Relocate column
mydat <- mydat |>
  relocate(date, .after = date_time) |>
  relocate(time, .after = date)
```

## group and summarize

#slice_head_tail_min_Max_sample...




fill function to imputation missing values below some non-missing 

```r
# Impute patients age by last age data available
dermatitis <- dermatitis |>
  arrange(opd_number, skin_date) |>
  group_by(opd_number) |>
  fill(age, .direction = "down") |>
  ungroup()
```