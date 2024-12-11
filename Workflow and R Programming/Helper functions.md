
[[A function to count the unique pt id:]]

note `sym(col_string)` can be used to refer column using string name. 

```r
# A function to return pt numbers along the analysis
report_pt_number <- function(data = mydat, col = "opd_number", time = 1) {
  n = length(unique(data[[sym(col)]]))
  print(n)
}

```


[[A function to plot proportion bar with significant]]

#list_column, #unnest

```r
# function plot_pct_trend
# select icd, intervials of dermatitis episode and
# disease of interests,
# Plot percentile trend by year
# Give comments as title.
plot_pct_trend <- function(icd = "L20|L23", date_interval = "0.25",
                           disease = "哮喘|鼻炎",
                           title_text = "2019-2024六年时间，过敏性皮炎患者中，伴随哮喘/鼻炎的患者人数迅速增加。") {
  derm_counts <- dermatitis |>
    filter(abs(date_diff) <= date_interval) |>
    filter(str_detect(skin_icd_full, derm_label_string)) |>
    select(opd_number, skin_year) |>
    distinct() |>
    group_by(skin_year) |>
    summarise(total_dermtitis_yrs = n())
  
  comorb_counts <- dermatitis |>
    filter(abs(date_diff) <= date_interval) |>
    filter(str_detect(comorb, disease)) |>
    select(opd_number, skin_year) |>
    distinct() |>
    group_by(skin_year) |>
    summarise(total_comorb_yrs = n())
  
  derm_counts <- derm_counts |>
    left_join(comorb_counts, by = "skin_year") 
  
  sig <- prop.trend.test(derm_counts$total_comorb_yrs, 
                         derm_counts$total_dermtitis_yrs, 
                         score = derm_counts$skin_year)
  # relabel_p value significance
  
  relabel_significance <- function(p) {
    if (p > 0.05) {
      return(paste0("p = ", signif(p, 2))) # Show the p-value rounded to 2 significant digits
    } else if (p <= 0.05 && p > 0.01) {
      return("p < 0.05")
    } else if (p <= 0.01 && p > 0.001) {
      return("p < 0.01")
    } else {
      return("p < 0.001")
    }
  }
  
  sig_result <- relabel_significance(sig$p.value)
  
  derm_counts <- derm_counts |>
    rowwise() |>
    mutate(
      CI_Proportion = list(binom.confint(total_comorb_yrs, total_dermtitis_yrs, methods = "wilson"))
    ) %>%
    unnest_wider(CI_Proportion)
  

  ggplot(derm_counts, aes(x = skin_year, y = mean, fill = factor(skin_year))) +
    geom_col(show.legend = FALSE
    ) +
    geom_text(
      aes(
        x = skin_year, y = mean,
        label = percent(mean, 0.1)
      ),
      hjust = -0.2,
      vjust = -0.5,
      size = 15
    ) +
    geom_errorbar(aes(ymin = lower, ymax = upper), 
                  width = 0.2) + 
    scale_x_continuous(breaks = c(2019:2024)) +
    scale_y_continuous(labels = percent_format(accuracy = 0.1)) +
    scale_fill_discrete_sequential("TealGrn") +
    labs(
      title = title_text,
      subtitle = paste(sig$method, ":", sig_result), 
      x = "年",
      y = "患者百分比"
    ) +
    theme_classic() +
    theme(text = element_text(size = 35))
}
```

