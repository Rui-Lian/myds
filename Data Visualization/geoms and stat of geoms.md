
| **Geom**                | **Description**                   | **Default `stat`** | **Other Allowed `stat` Options**    |
| ----------------------- | --------------------------------- | ------------------ | ----------------------------------- |
| `geom_point()`          | Scatter plot                      | `identity`         | None (always plots raw data as-is). |
| `geom_line()`           | Line chart                        | `identity`         | None (always plots raw data as-is). |
| `geom_smooth()`         | Add a smoothed trend line         | `smooth`           | `identity`, `quantile`              |
| `geom_bar()`            | Bar chart (counts by default)     | `count`            | `identity`, `bin`, `summary`        |
| `geom_col()`            | Bar chart (values specified)      | `identity`         | None (plots raw data as-is).        |
| `geom_histogram()`      | Histogram                         | `bin`              | `identity`, `count`, `density`      |
| `geom_boxplot()`        | Boxplot                           | `identity`         | `count`, `density`                  |
| `geom_violin()`         | Violin plot                       | `identity`         | `ydensity`                          |
| `geom_density()`        | Density plot                      | `density`          | `identity`, `count`                 |
| `geom_area()`           | Area plot                         | `identity`         | `count`, `density`, `bin`           |
| `geom_ribbon()`         | Ribbon plot                       | `identity`         | None (plots raw data as-is).        |
| `geom_tile()`           | Heatmap                           | `identity`         | `count`, `bin`                      |
| `geom_text()`           | Text annotations                  | `identity`         | None (plots raw data as-is).        |
| `geom_label()`          | Text with background box          | `identity`         | None (plots raw data as-is).        |
| `geom_hline()`          | Horizontal reference line         | `identity`         | None (plots raw data as-is).        |
| `geom_vline()`          | Vertical reference line           | `identity`         | None (plots raw data as-is).        |
| `geom_abline()`         | Line with slope and intercept     | `identity`         | None (plots raw data as-is).        |
| `geom_segment()`        | Line segment                      | `identity`         | None (plots raw data as-is).        |
| `geom_path()`           | Connected path (order matters)    | `identity`         | None (plots raw data as-is).        |
| `geom_polygon()`        | Polygon shapes                    | `identity`         | None (plots raw data as-is).        |
| `geom_sf()`             | Geometric shapes for `sf` objects | `identity`         | None (plots raw data as-is).        |
| `geom_rug()`            | Marginal rugs along axes          | `identity`         | None (plots raw data as-is).        |
| `geom_step()`           | Step chart                        | `identity`         | None (plots raw data as-is).        |
| `geom_jitter()`         | Scatter plot with jittered points | `identity`         | None (plots raw data as-is).        |
| `geom_errorbar()`       | Vertical error bars               | `identity`         | None (plots raw data as-is).        |
| `geom_errorbarh()`      | Horizontal error bars             | `identity`         | None (plots raw data as-is).        |
| `geom_dotplot()`        | Dot plot                          | `bindot`           | `bin`, `count`, `density`           |
| `geom_freqpoly()`       | Frequency polygon                 | `bin`              | `count`, `density`                  |
| `geom_density2d()`      | 2D density contours               | `density2d`        | `identity`, `bin`, `count`          |
| `geom_hex()`            | Hexbin plot                       | `bin`              | `count`, `density`                  |
| `geom_pointrange()`<br> | Point with error bars (y-axis)    | `identity`         | None (plots raw data as-is).        |




