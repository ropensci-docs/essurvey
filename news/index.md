# Changelog

## essurvey 1.0.8.9999

## essurvey 1.0.8

CRAN release: 2022-01-09

- Fixes URL creation bug
  ([\#53](https://github.com/ropensci/essurvey/issues/53))

## essurvey 1.0.7

CRAN release: 2021-03-22

- CRAN maintenance release. All vignettes are now precompiled to avoid
  errors when the ESS website breaks for some reason.
- `ess_email` environmental variable has been renamed to `ESS_EMAIL` to
  comply with Github Actions standards

## essurvey 1.0.6

CRAN release: 2021-01-27

- CRAN maintenance release to fix Solaris warnings
  `Warning in engine$weave(file, quiet = quiet, encoding = enc) : Pandoc (>= 1.12.3) and/or pandoc-citeproc not available. Falling back to R Markdown v1`
  on CRAN. Tested on Rhub and all passes OK, notifying CRAN.

- Removes automatic citation message when loading package. It’s actually
  annoying.

## essurvey 1.0.5

CRAN release: 2019-12-11

CRAN maintenance release to add more informative message when the status
code of the HTTP request of ‘www.europeansocialsurvey.org’ is more than
300.

### Minor changes

All tests/examples are now excluded from running on CRAN based on the
warning from Brian Ripley:

‘Packages which use Internet resources should fail gracefully with an
informative message if the resource is not available (and not give a
check warning nor error).’

They are all forced to run on Travis and Appveyor and this is made clear
on the `cran-comments.md`

## essurvey 1.0.4

CRAN release: 2019-11-04

CRAN maintenance check after release of ESS round 9.

## essurvey 1.0.3

CRAN release: 2019-10-15

### Breaking changes

- If you don’t know which format is available for a round/country,
  `import_*` and `download_*` functions now accept a NULL argument which
  runs through `'stata'`, `'spss'` and `'sas'` formats automatically. By
  default, `import_*` functions have now format set to `NULL` to
  automatically try the three different formats. This breaks backward
  dependency but only slightly where it had ‘stata’ set as default.

### New features

- Users can now download SDDF (weight data) for each country/round
  combination of files. Functions `show_sddf_cntrounds`,
  `import_sddf_country` and `download_sddf_country` are now introduced.
  For technical purposes, `show_sddf_cntrounds` needs for the user to
  have set their registered ESS email with `set_email`. \[#9\]

### Minor changes

- Bumps `haven` to minimum package version 2.1.1
- New package website at <https://docs.ropensci.org/essurvey>

### Internal

- `read_format_data` now tries to read data using `haven` but falls
  backs to `foreign` in case there’s an error. This should only work for
  SDDF data \[#38\].
- `read_format_data` and `read_sddf_data` now always return a list.
  Checking the length of data to return a data frame now happens within
  each `import_*` function.

### Bug fixes

- Removes an unnecessary if statement in `set_email` that didn’t allow
  to overwrite the email once set.

## essurvey 1.0.2

CRAN release: 2018-08-23

### Minor changes

- `show_country_rounds` checks if there are missing values and excludes
  them.

### Breaking changes

`import_all_cntrounds` and `import_country` returned incorrect countries
\[#31\]

## essurvey 1.0.1

CRAN release: 2018-06-02

### Minor changes

- `ess_email` is now checked that it is not `""` because it wasn’t
  raising an error before.

- Removes the `round` argument from `import_all_cntrounds` because it
  was a mistake. It already grabs the rounds internally.

## essurvey 1.0.1

CRAN release: 2018-06-02

Minor release

- Fixes test that checks the number of rounds that each country has.
  This test was a mistake because the rounds will change as time passes
  by and precise country rounds shouldn’t be tested.

## essurvey 1.0.0

CRAN release: 2018-04-06

The `ess` package has been renamed to `essurvey` for a name conflict
with Emacs Speaks Statistics (ESS). See R-pkg mailing list, the post
related to the release of ess-0-0-1.

### Breaking changes

- `ess_rounds` and `ess_all_rounds` are deprecated and will be removed
  in the next release. Use `import_rounds` instead \[#22\]

- `ess_country` and `ess_all_cntrounds` are deprecated and will be
  removed in the next release. Use `import_countries` instead \[#22\]

- The `your_email` argument name of `ess_*` functions has be changed to
  `ess_email` \[#23\]

### New features

- `import_rounds`, `import_all_rounds` and `download_rounds` have been
  introduced as replacements of `ess_rounds` and `ess_all_rounds`. Same
  changes were repeated for `ess_country` and `ess_all_cntrounds`
  \[#22\]

- `set_email` to set your email as environmental variable rather than
  write it in each call \[#23\]

- All requests to the ESS website are now done through HTTPS rather than
  HTTP \[#24\]

- Add package level documentation \[#20\]

### Minor changes

- `ess_email` had no default value but now has `NULL` as default \[#23\]

- The `format` argument is now checked through `match.arg` rather than
  manual check \[#25\]
