|                           |
| ------------------------- |
| comorbidity {comorbidity} |

```r
# Calculate CCI
result_cci <- comorbidity(mydat,
  id = "opd_number",
  code = "icd_three",
  map = "charlson_icd10_quan",
  assign0 = FALSE
)

# Reshape to long format and sum patient CCI.
result_cci <- result_cci |>
  pivot_longer(-opd_number, names_to = "comorb", values_to = "val") |>
  group_by(opd_number) |>
  mutate(cci = sum(val, na.rm = TRUE)) |>
  select(opd_number, cci) |>
  distinct()

# Join cci to mydat
mydat <- mydat |>
  left_join(result_cci, by = "opd_number")

report_pt_number()
```