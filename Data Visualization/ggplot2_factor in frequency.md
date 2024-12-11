```r
# fct_infreq
ggplot(penguins, aes(x = fct_infreq(species))) +
geom_bar()
```

