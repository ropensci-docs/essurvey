# Return available rounds for a country in the European Social Survey

Return available rounds for a country in the European Social Survey

## Usage

``` r
show_country_rounds(country)
```

## Arguments

- country:

  A character of length 1 with the full name of the country. Use
  [`show_countries`](https://docs.ropensci.org/essurvey/reference/show_countries.md)for
  a list of available countries.

## Value

numeric vector with available rounds for `country`

## Examples

``` r

if (FALSE) { # \dontrun{

show_country_rounds("Spain")

show_country_rounds("Turkey")

} # }
```
