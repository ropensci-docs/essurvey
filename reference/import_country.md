# Download integrated rounds separately for countries from the European Social Survey

Download integrated rounds separately for countries from the European
Social Survey

## Usage

``` r
import_country(country, rounds, ess_email = NULL, format = NULL)

import_all_cntrounds(country, ess_email = NULL, format = NULL)

download_country(
  country,
  rounds,
  ess_email = NULL,
  output_dir = getwd(),
  format = "stata"
)
```

## Arguments

- country:

  a character of length 1 with the full name of the country. Use
  [`show_countries`](https://docs.ropensci.org/essurvey/reference/show_countries.md)
  for a list of available countries.

- rounds:

  a numeric vector with the rounds to download. See
  [`show_rounds`](https://docs.ropensci.org/essurvey/reference/show_rounds.md)
  for all available rounds.

- ess_email:

  a character vector with your email, such as "your_email@email.com". If
  you haven't registered in the ESS website, create an account at
  <http://www.europeansocialsurvey.org/user/new>. A preferred method is
  to login through
  [`set_email`](https://docs.ropensci.org/essurvey/reference/set_email.md).

- format:

  the format from which to download the data. By default it is NULL for
  `import_*` functions and tries to read 'stata', 'spss' and 'sas' in
  the specific order. This can be useful if some countries don't have a
  particular format available. Alternatively, the user can specify the
  format which can either be 'stata', 'spss' or 'sas'. For the
  `download_*` functions it is set to 'stata' because the format should
  be specified before the downloading. When using `import_country` the
  data will be downloaded and read in the `format` specified. For
  `download_country`, the data is downloaded from the specified `format`
  (only 'spss' and 'stata' supported, see details).

- output_dir:

  a character vector with the output directory in case you want to only
  download the files using `download_country`. Defaults to your working
  directory. This will be interpreted as a **directory** and not a path
  with a file name.

## Value

for `import_country` if `length(rounds)` is 1, it returns a tibble with
the latest version of that round. Otherwise it returns a list of
`length(rounds)` containing the latest version of each round. For
`download_country`, if `output_dir` is a valid directory, it returns the
saved directories invisibly and saves all the rounds in the chosen
`format` in `output_dir`

## Details

Use `import_country` to download specified rounds for a given country
and import them to R. `import_all_cntrounds` will download all rounds
for a given country by default and `download_country` will download
rounds and save them in a specified `format` in the supplied directory.

The `format` argument from `import_country` should not matter to the
user because the data is read into R either way. However, different
formats might have different handling of the encoding of some questions.
This option was preserved so that the user can switch between formats if
any encoding errors are found in the data. For more details see the
discussion [here](https://github.com/ropensci/essurvey/issues/11). For
this particular argument, 'sas' is not supported because the data
formats have changed between ESS waves and separate formats require
different functions to be read. To preserve parsimony and format errors
between waves, the user should use 'spss' or 'stata'.

## Examples

``` r
if (FALSE) { # \dontrun{

set_email("your_email@email.com")

# Get first three rounds for Denmark
dk_three <- import_country("Denmark", 1:3)

# Only download the files, this will return nothing

temp_dir <- tempdir()

download_country(
 "Turkey",
 rounds = c(2, 4),
 output_dir = temp_dir
)

# By default, download_country downloads 'stata' files but
# you can also download 'spss' or 'sas' files.

download_country(
 "Turkey",
 rounds = c(2, 4),
 output_dir = temp_dir,
 format = 'spss'
)

# If email is not registered at ESS website, error will arise
uk_one <- import_country("United Kingdom", 5, "wrong_email@email.com")
# Error in authenticate(ess_email) : 
# The email address you provided is not associated with any registered user.
# Create an account at http://www.europeansocialsurvey.org/user/new

# If selected rounds don't exist, error will arise

czech_two <- import_country("Czech Republic", c(1, 22))

# Error in country_url(country, rounds) : 
# Only rounds ESS1, ESS2, ESS4, ESS5, ESS6, ESS7, ESS8 available
# for Czech Republic
} # }
```
