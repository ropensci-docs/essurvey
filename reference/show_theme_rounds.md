# Return available rounds for a theme in the European Social Survey

This function returns the available rounds for any theme from
[`show_themes`](https://docs.ropensci.org/essurvey/reference/show_themes.md).
However, contrary to
[`show_country_rounds`](https://docs.ropensci.org/essurvey/reference/show_country_rounds.md)
themes can not be downloaded as separate datasets. This and the
[`show_themes`](https://docs.ropensci.org/essurvey/reference/show_themes.md)
function serve purely for informative purposes.

## Usage

``` r
show_theme_rounds(theme)
```

## Arguments

- theme:

  A character of length 1 with the full name of the theme. Use
  [`show_themes`](https://docs.ropensci.org/essurvey/reference/show_themes.md)for
  a list of available themes.

## Value

numeric vector with available rounds for `country`

## Examples

``` r

if (FALSE) { # \dontrun{
chosen_theme <- show_themes()[3]

# In which rounds was the topic of 'Democracy' asked?
show_theme_rounds(chosen_theme)

# And politics?
show_theme_rounds("Politics")

} # }
```
