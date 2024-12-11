```r
# Create baseline data
# for each patient, the earliest date of dermatitis episode and
# the earliest time in that day
# Notice some patients have multiple diagnosis on that day
# Double counting occurs.
tb1_dat <- dermatitis |>
  group_by(opd_number) |>
  filter(skin_date == min(skin_date)) |>
  filter(time == min(time))

# Create cci as category
tb1_dat$cci_strata <- factor(tb1_dat$cci)

report_pt_number(data = tb1_dat)

# A string to select variables in table one
vars <- c(
  "gender", "age_min", "age_group", "skin_icd_three",
  "hypertension", "diabetes", "cci", "cci_strata"
)

tb1_dat <- tb1_dat |>
  select(all_of(vars)) |>
  distinct()

# Check double counting in tb1_dat
tb1_dat |>
  group_by(opd_number) |>
  summarise(n = n()) |>
  arrange(desc(n))
```


```r
tab1 <- CreateTableOne(vars = vars, strata = "gender", data = tb1_dat)

print(tab1)

tab1 <- as.data.frame(print(tab1))

write.csv(tab1, "table1.csv")
```
