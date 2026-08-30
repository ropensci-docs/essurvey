# Return available SDDF rounds for a country in the European Social Survey

Return available SDDF rounds for a country in the European Social Survey

## Usage

``` r
show_sddf_cntrounds(country, ess_email = NULL)
```

## Arguments

- country:

  A character of length 1 with the full name of the country. Use
  [`show_countries`](https://docs.ropensci.org/essurvey/reference/show_countries.md)
  for a list of available countries.

- ess_email:

  a character vector with your email, such as "your_email@email.com". If
  you haven't registered in the ESS website, create an account at
  <http://www.europeansocialsurvey.org/user/new>. A preferred method is
  to login through
  [`set_email`](https://docs.ropensci.org/essurvey/reference/set_email.md).

## Value

numeric vector with available rounds for `country`

## Details

SDDF data are the equivalent weight data used to analyze the European
Social Survey properly. For more information, see the details section of
[`import_sddf_country`](https://docs.ropensci.org/essurvey/reference/import_sddf_country.md).
As an exception to the `show_*` family of functions, `show_sddf rounds`
needs your ESS email to check which rounds are available. Be sure to add
it with
[`set_email`](https://docs.ropensci.org/essurvey/reference/set_email.md).

## Examples

``` r

if (FALSE) { # \dontrun{
set_email("your_email@email.com")

show_sddf_cntrounds("Spain")
} # }
```
