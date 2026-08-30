# Download SDDF data by round for countries from the European Social Survey

Download SDDF data by round for countries from the European Social
Survey

## Usage

``` r
import_sddf_country(country, rounds, ess_email = NULL, format = NULL)

import_all_sddf_cntrounds(country, ess_email = NULL, format = NULL)

download_sddf_country(
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
  [`show_sddf_cntrounds`](https://docs.ropensci.org/essurvey/reference/show_sddf_cntrounds.md)
  for all available rounds for any given country.

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
  be specified before downloading. Setting it to `NULL` will iterate
  over 'stata', 'spss' and 'sas' and download the first that is
  available. When using `import_country` the data will be downloaded and
  read in the `format` specified. For `download_country`, the data is
  downloaded from the specified `format` (only 'spss' and 'stata'
  supported, see details).

- output_dir:

  a character vector with the output directory in case you want to only
  download the files using `download_sddf_country`. Defaults to your
  working directory. This will be interpreted as a **directory** and not
  a path with a file name.

## Value

for `import_sddf_country` if `length(rounds)` is 1, it returns a tibble
with the latest version of that round. Otherwise it returns a list of
`length(rounds)` containing the latest version of each round. For
`download_sddf_country`, if `output_dir` is a valid directory, it
returns the saved directories invisibly and saves all the rounds in the
chosen `format` in `output_dir`

## Details

SDDF data (Sample Design Data Files) are data sets that contain
additional columns with the sample design and weights for a given
country in a given round. These additional columns are required to
perform any complex weighted analysis of the ESS data. Users interested
in using this data should read the description of SDDF files
[here](http://www.europeansocialsurvey.org/methodology/ess_methodology/sampling.md)
and should read
[here](http://www.europeansocialsurvey.org/data/download_sample_data.md)
for the sampling design of the country of analysis for that specific
round.

Use `import_sddf_country` to download the SDDF data by country into R.
`import_all_sddf_cntrounds` will download all available SDDF data for a
given country by default and `download_sddf_country` will download SDDF
data and save them in a specified `format` in the supplied directory.

The `format` argument from `import_country` should not matter to the
user because the data is read into R either way. However, different
formats might have different handling of the encoding of some questions.
This option was preserved so that the user can switch between formats if
any encoding errors are found in the data. For more details see the
discussion [here](https://github.com/ropensci/essurvey/issues/11).

Additionally, given that the SDDF data is not very complete, some
countries do not have SDDF data in Stata or SPSS formats. For that
reason, the `format` argument is not used in `import_sddf_country`.
Internally, `Stata` is chosen over `SPSS` and `SPSS` over `SAS` in that
order of preference.

For this particular argument, 'sas' is not supported because the data
formats have changed between ESS waves and separate formats require
different functions to be read. To preserve parsimony and format errors
between waves, the user should use 'stata' or 'spss'.

Starting from round 7 (including), the ESS switched the layout of SDDF
data. Before the rounds, SDDF data was published separately by
wave-country combination. From round 7 onwards, all SDDF data is
released as a single integrated file with all countries combined for
that given round. `import_sddf_country` takes care of this nuance by
reading the data and filtering the chosen country automatically.
`download_sddf_country` downloads the raw file but also reads the data
into memory to subset the specific country requested. This process
should be transparent to the user but beware that reading/writing the
data might delete some of it's properties such as dropping the labels or
label attribute.

## Examples

``` r
if (FALSE) { # \dontrun{

set_email("your_email@email.com")

sp_three <- import_sddf_country("Spain", 5:6)

show_sddf_cntrounds("Spain")

# Only download the files, this will return nothing

temp_dir <- tempdir()

download_sddf_country(
 "Spain",
 rounds = 5:6,
 output_dir = temp_dir
)

# By default, download_sddf_country downloads 'stata' files but
# you can also download 'spss' or 'sas' files.

download_sddf_country(
 "Spain",
 rounds = 1:8,
 output_dir = temp_dir,
 format = 'spss'
)

} # }
```
