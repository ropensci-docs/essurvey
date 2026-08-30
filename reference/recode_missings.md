# Recode pre-defined missing values as NA

This function is not needed any more, please see the details section.

## Usage

``` r
recode_missings(ess_data, missing_codes)

recode_numeric_missing(x, missing_codes)

recode_strings_missing(y, missing_codes)
```

## Arguments

- ess_data:

  data frame or
  [`tibble`](https://tibble.tidyverse.org/reference/tibble.html) with
  data from the European Social Survey. This data frame should come
  either from
  [`import_rounds`](https://docs.ropensci.org/essurvey/reference/import_rounds.md),
  [`import_country`](https://docs.ropensci.org/essurvey/reference/import_country.md)
  or read with
  [`read_dta`](https://haven.tidyverse.org/reference/read_dta.html) or
  [`read_spss`](https://haven.tidyverse.org/reference/read_spss.html).
  This is the case because it identifies missing values using
  [`labelled`](https://haven.tidyverse.org/reference/labelled.html)
  classes.

- missing_codes:

  a character vector with values 'Not applicable', 'Refusal', 'Don't
  Know', 'No answer' or 'Not available'. By default all values are
  chosen. Note that the wording is case sensitive.

- x:

  a [`labelled`](https://haven.tidyverse.org/reference/labelled.html)
  numeric

- y:

  a character vector

## Value

The same data frame or
[`tibble`](https://tibble.tidyverse.org/reference/tibble.html) but with
values 'Not applicable', 'Refusal', 'Don't Know', 'No answer' and 'Not
available' recoded as NA.

## Details

Data from the European Social Survey is always accompanied by a script
that recodes the categories 'Not applicable', 'Refusal', 'Don't Know',
'No answer' and 'Not available' to missing. This function recodes these
categories to NA

The European Social Survey now provides these values recoded
automatically in Stata data files. These missing categories are now read
as missing values by
[`read_dta`](https://haven.tidyverse.org/reference/read_dta.html),
reading the missing categories correctly from Stata.For an example on
how these values are coded, see
[here](https://github.com/ropensci/essurvey/issues/35).

Old details:

When downloading data directly from the European Social Survey's
website, the downloaded .zip file contains a script that recodes some
categories as missings in Stata and SPSS formats.

For recoding numeric variables `recode_numeric_missings` uses the labels
provided by the
[`labelled`](https://haven.tidyverse.org/reference/labelled.html) class
to delete the labels matched in `missing_codes`. For the character
variables matching is done with the underlying number assigned to each
category, namely 6, 7, 8, 9 and 9 for 'Not applicable', Refusal', 'Don't
Know', No answer' and 'Not available'.

The functions are a direct translation of the Stata script that comes
along when downloading one of the rounds. The Stata script is the same
for all rounds and all countries, meaning that these functions work for
all rounds.

## Examples

``` r
if (FALSE) { # \dontrun{
seven <- import_rounds(7, your_email)

attr(seven$tvtot, "labels")
mean(seven$tvtot, na.rm = TRUE)

names(table(seven$lnghom1))
# First three are actually missing values

seven_recoded <- recode_missings(seven)

attr(seven_recoded$tvtot, "labels")
# All missings have been removed
mean(seven_recoded$tvtot, na.rm = TRUE)

names(table(seven_recoded$lnghom1))
# All missings have been removed

# If you want to operate on specific variables
# you can use other recode_*_missing 

seven$tvtot <- recode_numeric_missing(seven$tvtot)

# Recode only 'Don't know' and 'No answer' to missing
seven$tvpol <- recode_numeric_missing(seven$tvpol, c("Don't know", "No answer"))


# The same can be done with recode_strings_missing
} # }
```
