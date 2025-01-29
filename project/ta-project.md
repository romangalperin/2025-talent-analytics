2025 Talent analytics term project
================

## Project overview

**NOTE: While this case uses real data from a real organization, the
context and the premise for the analysis described below are
hypothetical and are presented here purely for educational purposes.**

### Context

The U.S. Patent and Trademark Office (USPTO) is one of the most
important organizations for supporting innovation and economic growth.
The USPTO employs over 10,000 patent examiners whose primary task is to
assess inventions for patentability and issue patents when appropriate.

Inventors submit patent applications, pay the associated fees and
receive a decision from a patent examiner. If all of the inventor’s
claims made in a patent application are allowed by the examiner—i.e.,
determined to be novel and non-obvious in light of prior inventions—the
examiner issues a patent.

If some or all of the claims are rejected as not meeting the
patentability criteria, the examiner issues a formal rejection of the
application, which presents the applicant with a choice: abandon the
application and stop the process, or continue the process by revising
the application and resubmitting it to the agency for another round of
consideration. The latter option is associated with additional fees, but
is virtually always open: the applicant can continue to reapply with no
limit on the number of attempts. (This process is described in more
detail
[here](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2995674).)

### The challenge

Since innovation is dynamic and because patent rights can be highly
valuable for inventors, the timing of the USPTO’s decisions on patent
applications is a sensitive issue for inventors. The USPTO has faced
some pressure from policymakers and regulators to address the problem of
long review times. The agency is interested in understanding what
affects the examination time—the time from the date the application is
filed until a definitive decision is made. Understanding the causes and
the variation in the examination time can help reduce the backlog.

### Inequities among examiners

The agency suspects—and has some indirect evidence—that examiners’ work,
mobility across units, promotion across pay grades and attrition differ
systematically by demographic characteristics. Of special concern are
patterns related to examiner’s gender and race/ethnicity, not only
because such differences may pose obvious ethical challenges, but also
because they increase the risk of legal liability for the agency. The
USPTO would like to understand what, if any, patterns in examiners’
work, mobility, promotion and attrition vary systematically by race
and/or gender.

## Team project

Your team’s goal is to perform the analysis of the agency’s data as a
consulting team would. Base on the analysis, you will write a short
report (no longer than 10 pages including all figures table and
references, if any). Your analysis will have two parts.

### Part 1

In this hands-on, empirical part, you will focus on **one or more** of
the following questions:

- What are the organizational and social factors associated with the
  length of patent application prosecution?
- What are the organizational and social factors associated with
  examiner attrition?
- What is the role of gender, race and ethnicity here in the processes
  underlying the question above?

Offer convincing analysis, as well as projections and related
recommendations.

### Part 2

Conduct an exploratory survey of current offerings on people analytics:
apps, methodologies, SaaS solutions, AI tools, etc. The preference
should be given to recent and new tools and services, e.g., those that
use generative AI or new developments in behavioral sciences. Try to
avoid generic consulting offerings disguised as AI/science adjacent.
Focus on one product or firm, if possible. Feel free to reach out to
their sales team to learn more about the product. Report the following:

- How would a given set of tools/technology help with the challenges
  identified above? Be as specific as possible.
- What are your potential concerns about the tool/technology you are
  focusing on, from the perspective of research design and quality of
  evidence topics that we have covered in this course? Be as specific as
  you can.
- \[Bonus\] Propose your own tool, based on OpenAI’s offerings (APIs,
  Custom GPTs, fine-tuning, etc.). Be as specific as possible about the
  features, technical setup and the benefits relative to the existing
  offerings.

## Timing

You can and should start working on the project as soon as your group is
formed. Our weekly exercises will help you build the analysis strategy
and move you toward the project’s goal.

## Data

The data on examiners and patent applications come from various public
sources. I have modified some of the source files to make them smaller
and more manageable, but feel free to use the original sources if you
feel compelled.

## R packages (libraries)

R packages I recommend for working with the data:

- `lubridate` for working with dates
- `stringr` for working with character strings
- `skimr` for quick summaries of data columns

### Patent applications

The largest data file is on patent applications. It comes from the
[USPTO 2016 PatEx
dataset](https://www.uspto.gov/ip-policy/economic-research/research-datasets/patent-examination-research-dataset-public-pair).
The full data file takes between 0.5Gb and 1Gb of memory, depending on
how you load it, so I have created a smaller subsample of the data for
your convenience, using the following restrictions:

- The year of `filing_date` is 2000 or later
- Only 4 of the 9 [Technology
  Centers](https://www.uspto.gov/patents/contact-patents/patent-technology-centers-management)
  comprising the agency are included: 1600, 1700, 2100 and 2400
- Only 15 relevant variables are included (see [PatEx data
  dictionary](https://www.uspto.gov/sites/default/files/documents/Appendix%20A.pdf))

``` r
app_data_raw %>%
  tbl_vars()
```

    ## <dplyr:::vars>
    ## [1] "application_number" "filing_date"        "examiner_id"       
    ## [4] "au"                 "disposal_type"      "tc"                
    ## [7] "gender"             "race"               "earliest_date"

``` r
app_data_raw
```

    ## # A tibble: 2,018,477 × 9
    ##    application_number filing_date examiner_id    au disposal_type    tc gender
    ##    <chr>              <date>            <dbl> <dbl> <chr>         <dbl> <chr> 
    ##  1 08284457           2000-01-26        96082  1764 ISS            1700 female
    ##  2 08413193           2000-10-11        87678  1764 ISS            1700 <NA>  
    ##  3 08531853           2000-05-17        63213  1752 ISS            1700 female
    ##  4 08637752           2001-07-20        73788  1648 ISS            1600 female
    ##  5 08682726           2000-04-10        77294  1762 ABN            1700 male  
    ##  6 08687412           2000-04-28        68606  1734 ISS            1700 female
    ##  7 08716371           2004-01-26        89557  1627 PEND           1600 female
    ##  8 08765941           2000-06-23        97543  1645 ABN            1600 female
    ##  9 08776818           2000-02-04        98714  1637 ABN            1600 female
    ## 10 08809677           2002-02-20        65530  1723 ISS            1700 female
    ## # ℹ 2,018,467 more rows
    ## # ℹ 2 more variables: race <chr>, earliest_date <date>
