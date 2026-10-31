# Week 10: Fish Analysis


## Fish Scale Analysis

Load the tidyverse and the dataset

``` r
#install.packages("tidyverse")
library(tidyverse)
```

    Warning: package 'tidyverse' was built under R version 4.5.3

    Warning: package 'ggplot2' was built under R version 4.5.3

    Warning: package 'tibble' was built under R version 4.5.3

    Warning: package 'tidyr' was built under R version 4.5.3

    Warning: package 'readr' was built under R version 4.5.3

    Warning: package 'purrr' was built under R version 4.5.3

    Warning: package 'dplyr' was built under R version 4.5.3

    Warning: package 'stringr' was built under R version 4.5.3

    Warning: package 'forcats' was built under R version 4.5.3

    Warning: package 'lubridate' was built under R version 4.5.3

    ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ✔ dplyr     1.2.1     ✔ readr     2.2.0
    ✔ forcats   1.0.1     ✔ stringr   1.6.0
    ✔ ggplot2   4.0.3     ✔ tibble    3.3.1
    ✔ lubridate 1.9.5     ✔ tidyr     1.3.2
    ✔ purrr     1.2.2     
    ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ✖ dplyr::filter() masks stats::filter()
    ✖ dplyr::lag()    masks stats::lag()
    ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
fish_data <- read_csv("../data/Gaeta_etal_CLC_data.csv")
```

    Rows: 4033 Columns: 6
    ── Column specification ────────────────────────────────────────────────────────
    Delimiter: ","
    chr (2): lakeid, annnumber
    dbl (4): fish_id, length, radii_length_mm, scalelength

    ℹ Use `spec()` to retrieve the full column specification for this data.
    ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

Summary of fish scale statistics:

``` r
scale_statistics <- fish_data |>
  group_by(lakeid) |>
  summarize(min_scale_length = min(scalelength, na.rm = TRUE),
            max_scale_length = max(scalelength, na.rm = TRUE),
            mean_scale_length = mean(scalelength, na.rm = TRUE))
```

Create a new data frame that does not include fish with scale lengths of
less than 1 mm and save new dataframe as CSV

Use the `write_csv()` function to save this new data frame as a CSV
file. It should be in an appropriate sub-directory.

Commit this change to version control with a good commit message.

Once you’ve made the commit, push the commit to your repo. Pop over to
GitHub to ensure that the `.qmd` file and the new dataset are there.

``` r
filtered_fish_data <- fish_data |>
  filter(scalelength>=1)
getwd()
```

    [1] "C:/Users/mv214/OneDrive - University of Arizona/Documents/GitHub/VonRotz_DataWrangling/Week 10-Version Control/code"

``` r
write.csv(filtered_fish_data, file= file.path("../data", "filtered_fish_data.csv"))
```

Question 4 (a-g): made plot, saved it “../data/visuals”, rendered
document, and committed new code

``` r
ggplot(fish_data, aes(x = scalelength)) +
  geom_histogram(bins=80)+
  labs(x= "Scale Length (mm)", y= "Count")+
  theme_classic()
```

![](fishanalysis_files/figure-commonmark/unnamed-chunk-4-1.png)

``` r
ggsave(filename= file.path("../data/visuals", "scale_hist_by_length.jpg"))
```

    Saving 7 x 5 in image
