GPC Breast Cancer Data Quality Reporting
========================================

by Dan Connolly, with Russ Waitman, Tamara McMahon, and Vince Leonardo  
[Medical Informatics Division, Univeristy of Kansas Medical Center][MI]

[MI]: http://informatics.kumc.edu/

Copyright (c) 2015 Univeristy of Kansas Medical Center  
Share and Enjoy according to the terms of the MIT Open Source License.

## Background

On 23 Dec 2014, GPC honest brokers were requested to run a breast cancer cohort query
and submit results (see `bc_qa2.Rmd` for details). All participating sites have
now done so, and we are evaluating the results ([227]) using automated reports
built with [R Markdown][].

[227]: https://informatics.gpcnetwork.org/trac/Project/ticket/227
[R Markdown]: http://rmarkdown.rstudio.com/

An initial QA report was sent to each site 23 Feb 2014.

## Site Usage

In future iterations, sites are encouraged to run this report on their own before sumitting:

 1. Build *Query Terms and Exclusion Criteria* article
    - Run (i.e. knit) `bc_qa2.Rmd`
    - output: `bc_terms_results.RData`
 3. Build *QA for SITE* article
    1. Use [DataBuilder][] or equivalent to generate sqlite file.
    2. Copy `dataset-example.R` to `dataset.R` and edit filename etc.
    3. Run (i.e. knit) `bc_excl.Rmd`


[DataBuilder]: https://informatics.gpcnetwork.org/trac/Project/wiki/BuilderSaga

## Central Usage

As new submissions come in, members of the breast cancer research team can
reproduce the analysis of data from all sites:

 1. Fetch all the data files.
    - Knit `bc_fetch.Rmd` to build `bc_fetch_results.Rmd`
 2. Build *Query Terms and Exclusion Criteria* article as above
 3. Build any *QA for SITE* articles you like, using `dataset.R` as below.
 4. Build *Data by Site* presentation
    - Open `bc_qa_p1.Rpres` in R Studio and use the presentation tab.


```
load("bc_fetch_results.RData")

SITE <- 'KUMC'  # Salt to taste

(function (s) {
  list(
    conn=fetch$site.data(s),
    about=subset(fetch$dataset, site == s)
  )
})(SITE)
```
