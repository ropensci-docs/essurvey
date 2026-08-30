# Return countries that participated in **all** of the specified rounds.

Return countries that participated in **all** of the specified rounds.

## Usage

``` r
show_rounds_country(rounds, participate = TRUE)
```

## Arguments

- rounds:

  A numeric vector specifying the rounds from which to return the
  countries. Use
  [`show_rounds`](https://docs.ropensci.org/essurvey/reference/show_rounds.md)for
  a list of available rounds.

- participate:

  A logical that controls whether to show participating countries in
  that/those rounds or countries that didn't participate. Set to `TRUE`
  by default.

## Value

A character vector with the country names

## Details

`show_rounds_country` returns the countries that participated in **all**
of the specified rounds. That is, `show_rounds_country(1:2)` will return
countries that participated both in round 1 and round 2. Conversely, if
`participate = FALSE` it will return the countries that did not
participate in **both** round 1 and round 2.

## Examples

``` r

if (FALSE) { # \dontrun{

# Return countries that participated in round 2

show_rounds_country(2)

# Return countries that participated in all rounds

show_rounds_country(1:8)

# Return countries that didn't participate in the first three rounds

show_rounds_country(1:3, participate = FALSE)

} # }
```
