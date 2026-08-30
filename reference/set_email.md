# Save your ESS email as an environment variable

Save your ESS email as an environment variable

## Usage

``` r
set_email(ess_email)
```

## Arguments

- ess_email:

  a character string with your registered email.

## Details

You should only run `set_email()` once and every `import_` and
`download_` function should work fine. Make sure your email is
registered at <http://www.europeansocialsurvey.org/> before setting the
email.

## Examples

``` r

if (FALSE) { # \dontrun{
set_email("my_registered@email.com")

import_rounds(1)
} # }
```
