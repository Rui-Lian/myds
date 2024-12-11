## Network strucutre analysis and comorbidity

To conduct a formal analysis of the network structure of comorbidities,
several methodologies can be employed, leveraging graphical models and
network analysis techniques. Here’s a structured approach based on
recent studies and best practices in the field.

```r
# Based on dermatitis dataset
# Select data set from mydat
network_dat <- mydat |>
  filter(opd_number %in% dermatitis$opd_number)

report_pt_number(network_dat)
```

#igraph_package #pairs #edge_list

```r
# Filter and prepare the dataset
tmp <- network_dat %>%
  select(opd_number, icd_three) %>%
  distinct() %>%
  filter(!str_detect(icd_three, "L26|L22|L24")) |>
  mutate(seen = 1)

# Find all pairs of ICD codes for each patient
pairs <- tmp %>%
  group_by(opd_number) %>%
  summarise(
    Pairs = list(
      if (length(icd_three) > 1) {
        as.data.frame(t(combn(icd_three, 2)), stringsAsFactors = FALSE)
      } else {
        NULL
      }
    ),
    .groups = "drop"
  ) %>%
  filter(!is.null(Pairs)) %>% # Remove rows where Pairs is NULL
  unnest(Pairs, names_repair = "unique")

# Change V2 to icd10 Major
# icd 10 table from icd10Hierarchy in icdcoder package
# Select threedigit and major columns
icd10 <- icd10Hierarchy |>
  select(threedigit, major)

# Another option to join icd names in Chinese
icd10_cn <- read.table("disease.csv")

pairs <- pairs |>
  left_join(icd10_cn, by = c("V1" = "V1")) |>
  distinct()

# Remove V2 and use major as new V2
pairs <- pairs |>
  select(-V1) |>
  rename(
    "V1" = "V2.x",
    "V2" = "V2.y"
  ) |>
  distinct()

# Aggregate to get the edge list (weighted by co-occurrence frequency)
edge_list <- pairs %>%
  group_by(V1, V2) %>%
  summarise(Weight = n(), .groups = "drop") %>%
  arrange(desc(Weight)) %>%
  filter(str_detect(V1, derm_label_string)) %>%
  drop_na() |> 
  group_by(V1) %>%
  mutate(n = sum(Weight), 
         pct = Weight/n) |>
  arrange(desaturate(pct)) |>
  mutate(pct_accum = cumsum(pct)) |>
  slice_max(order_by = Weight, n = 15) %>%
  ungroup()

# Create a graph object
g <- graph_from_data_frame(edge_list, directed = FALSE)

# Compute the degree for each node and map it to size
V(g)$size <- degree(g) # Th

# Assign the major ICD code as the vertex name
V(g)$name <- unique(c(edge_list$V1, edge_list$V2)) # Set the ICD major names as vertex names

# Plot the network
set.seed(38360) # For reproducibility
ggraph(g, layout = "fr", niter = 500) +
  geom_edge_link(aes(alpha = Weight),
    color = "grey70",
    show.legend = FALSE
  ) +
  geom_node_point(aes(size = size),
    color = "orange",
    show.legend = FALSE
  ) + # Map size to degree
  geom_node_text(aes(label = name), vjust = 1.5, size = 8, color = "steelblue") +
  theme_void() +
  labs(title = "皮炎ICD代码下的相关合并症网络结构图分析") +
  theme(plot.title = element_text(size = 30, face = "bold")) +
  scale_size_continuous(range = c(3, 10)) # Adjust the range for node size scaling

ggsave("comorb_net.png", width = 10, height = 6.18, units = "in", dpi = 300)
```
