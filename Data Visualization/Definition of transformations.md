In **ggplot2**, a **stat** (short for statistical transformation) processes the raw data before it is passed to the geom for rendering. Here's a breakdown of the commonly used `stat` transformations and their meanings. 

> [!WARNING]
> This is a draft subject to further modification. 

[[Callout message in Obsidian]]

## How to Choose a Stat:
- **Distributions**: Use `bin`, `density`, or `count` to visualize the frequency or distribution of data.
- **Trend Lines**: Use `smooth` or `quantile` to add predictive or regression curves.
- **Summaries**: Use `summary` or `identity` to directly visualize data summaries or raw data.
- **Spatial Data**: Use `sf` for geospatial visualizations.

## **`identity`**


**`identity`**
   - **Description**: Does not transform the data (plots it as-is).
   - **Used With**: Most geoms (default for many).
   - **Purpose**: Directly map data to aesthetics without processing.

## **`count`**



 - **Description**: Counts the number of observations in each category or group.
   - **Used With**: `geom_bar`
   - **Purpose**: Generate bar charts that reflect the frequency of each category.

## **`summary`**

**`summary`**
   - **Description**: Summarizes data by a function (e.g., mean, median).
   - **Used With**: Custom configurations, occasionally with `geom_bar`.
   - **Purpose**: Compute summaries like averages for visualization.

## **`quantile`**

**`quantile`**
   - **Description**: Calculates quantile regression fits.
   - **Used With**: `geom_smooth` (optionally).
   - **Purpose**: Add quantile regression lines to visualize trends.

## **`bin`**

 **`bin`**
   - **Description**: Divides data into bins and computes the count of observations in each bin.
   - **Used With**: `geom_histogram`, `geom_freqpoly`, `geom_dotplot`, `geom_hex`
   - **Purpose**: Visualize distributions by grouping continuous data into intervals.

**`bin2d`**
   - **Description**: Similar to `bin`, but creates 2D bins for two continuous variables.
   - **Used With**: `geom_bin2d`, `geom_hex`
   - **Purpose**: Aggregate data into 2D bins for visualizing relationships.

**`summary_bin`**
   - **Description**: Groups data into bins and applies a summary function.
   - **Used With**: Custom configurations (e.g., for binned averages).
   - **Purpose**: Aggregate data into bins and compute statistics for each bin.

## **`density`**

**`density`**
   - **Description**: Estimates the probability density function (PDF) of a continuous variable.
   - **Used With**: `geom_density`, `geom_violin`
   - **Purpose**: Visualize the distribution of data using smoothed density curves.

**`ydensity`**
   - **Description**: Calculates density estimates along the y-axis for each group.
   - **Used With**: `geom_violin`
   - **Purpose**: Create violin plots showing density distributions split by a grouping variable.

**`density2d`**
   - **Description**: Computes 2D density estimates and represents them as contour lines.
   - **Used With**: `geom_density2d`
   - **Purpose**: Visualize density in two dimensions with contour plots.



## **`ecdf`**


**`ecdf`**
   - **Description**: Computes the empirical cumulative distribution function (ECDF).
   - **Used With**: `stat_ecdf` (no geom equivalent)
   - **Purpose**: Visualize cumulative distributions.

## **`smooth`**

**`smooth`**
   - **Description**: Computes a smoothed conditional mean using methods like LOESS or linear regression.
   - **Used With**: `geom_smooth`
   - **Purpose**: Add trend lines with optional confidence intervals.


## **`function`**
   - **Description**: Plots a mathematical function over the data range.
   - **Used With**: `geom_function`
   - **Purpose**: Add custom mathematical curves to plots.

## **`sf`**
   - **Description**: Handles spatial data in the `sf` format for geospatial visualization.
   - **Used With**: `geom_sf`
   - **Purpose**: Render spatial objects like polygons, points, or lines.



