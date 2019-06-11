**Extract Publication Data**
============================

Keeping accurate and up-to-date information regarding the output from an
author / research group can be a time consuming task, however remains
essential in order to evaluate the research impact. There are multiple
respositories on-line such as PubMed or CrossRef which store this
information, and can already be accessed using an API in R in order to
extract this data on an automatic basis.

There are an excellent packages that already exist to access this data -
[RISmed](https://cran.r-project.org/web/packages/RISmed/RISmed.pdf) for
PubMed and [rcrossref](https://github.com/ropensci/rcrossref) for
CrossRef. While these provide a vast quantity of useful information,
this is often outwith a dataframe/tibble format and so requires a
significant quantity of post-processing to otherwise achieve an easily
usable output.

 

**1. Extract Data**
-------------------

The functions `extract_pmid()` (PubMed) and `extract_doi()` (CrossRef)
use unique identifiers to extract important information regarding
publications. This can be used for the purposes of citation, cataloguing
publications, or for further evalauation of impact (see **ImpactR:
Citations**).

However, it should be noted that the information extracted is dependent
on the accuracy and completeness of the information within these
repositories. Therefore, some additional editing may be required to
remove heterogenity / make corrections / supply missing data.

### **`extract_pmid()`**

The `extract_pmid()` function only requires a vector/list of PubMed
identification numbers, and uses the
[RISmed](https://cran.r-project.org/web/packages/RISmed/RISmed.pdf)
package to extract publication information.

The function will automatically extract the authors (`auth_group`,
`auth_n`, `authors`), and the associated almetric score (`altmetric`).
However, this functionality has been made optional as it can extend the
run time of the function (particularly in the case of a large number of
authors).

``` r
# Example output from user_roles_n()
out_pubmed <- extract_pmid(pmid = c(26769786, 26195471, 30513129),
                            get_auth = TRUE, get_almetric = FALSE, get_impact = FALSE)
```

<div style="border: 1px solid #ddd; padding: 5px; overflow-x: scroll; width:1000; ">
<table class="table table-striped" style="width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
pmid
</th>
<th style="text-align:left;">
author\_group
</th>
<th style="text-align:left;">
type
</th>
<th style="text-align:left;">
title
</th>
<th style="text-align:right;">
year
</th>
<th style="text-align:left;">
journal\_full
</th>
<th style="text-align:left;">
journal\_abbr
</th>
<th style="text-align:left;">
volume
</th>
<th style="text-align:left;">
issue
</th>
<th style="text-align:left;">
pages
</th>
<th style="text-align:left;">
doi
</th>
<th style="text-align:left;">
journal\_issn
</th>
<th style="text-align:right;">
cite\_pm
</th>
<th style="text-align:right;">
auth\_n
</th>
<th style="text-align:left;">
author
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
30513129
</td>
<td style="text-align:left;">
STARSurg Collaborative
</td>
<td style="text-align:left;">
Paper
</td>
<td style="text-align:left;min-width: 6in; ">
Prognostic model to predict postoperative acute kidney injury in
patients undergoing major gastrointestinal surgery based on a national
prospective observational cohort study.
</td>
<td style="text-align:right;">
2018
</td>
<td style="text-align:left;">
BJS open
</td>
<td style="text-align:left;">
BJS Open
</td>
<td style="text-align:left;">
2
</td>
<td style="text-align:left;">
6
</td>
<td style="text-align:left;">
400-410
</td>
<td style="text-align:left;">
10.1002/bjs5.86
</td>
<td style="text-align:left;">
2474-9842
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
1784
</td>
<td style="text-align:left;min-width: 6in; ">
Nepogodiev D, Walker K, Glasbey JC, Drake TM, Bora…
</td>
</tr>
<tr>
<td style="text-align:left;">
26769786
</td>
<td style="text-align:left;">
STARSurg Collaborative
</td>
<td style="text-align:left;">
Paper
</td>
<td style="text-align:left;min-width: 6in; ">
Outcomes After Kidney injury in Surgery (OAKS): protocol for a
multicentre, observational cohort study of acute kidney injury following
major gastrointestinal and liver surgery.
</td>
<td style="text-align:right;">
2016
</td>
<td style="text-align:left;">
BMJ open
</td>
<td style="text-align:left;">
BMJ Open
</td>
<td style="text-align:left;">
6
</td>
<td style="text-align:left;">
1
</td>
<td style="text-align:left;">
e009812
</td>
<td style="text-align:left;">
10.1136/bmjopen-2015-009812
</td>
<td style="text-align:left;">
2044-6055
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
40
</td>
<td style="text-align:left;min-width: 6in; ">
Bath M, Glasbey J, Claireaux H, Drake T, Gundogan …
</td>
</tr>
<tr>
<td style="text-align:left;">
26195471
</td>
<td style="text-align:left;">
STARSurg Collaborative
</td>
<td style="text-align:left;">
Paper
</td>
<td style="text-align:left;min-width: 6in; ">
Determining Surgical Complications in the Overweight (DISCOVER): a
multicentre observational cohort study to evaluate the role of obesity
as a risk factor for postoperative complications in general surgery.
</td>
<td style="text-align:right;">
2015
</td>
<td style="text-align:left;">
BMJ open
</td>
<td style="text-align:left;">
BMJ Open
</td>
<td style="text-align:left;">
5
</td>
<td style="text-align:left;">
7
</td>
<td style="text-align:left;">
e008811
</td>
<td style="text-align:left;">
10.1136/bmjopen-2015-008811
</td>
<td style="text-align:left;">
2044-6055
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:left;min-width: 6in; ">
Nepogodiev D, Chapman SJ, Glasbey J, Kelly M, Khat…
</td>
</tr>
</tbody>
</table>
</div>
In general, it appears that the information on PubMed tends to be the
most accurate/up-to-date, however the Digital Object Identifier (DOI)
occationally is not updated to reflect the final DOI for the paper (this
can either be amended or the publisher contacted to correct).

 

### **`extract_doi()`**

The `extract_doi()` function only requires a vector/list of Digital
Object Identifiers (DOI), and uses the
[rcrossref](https://github.com/ropensci/rcrossref) package to extract
publication information.

The function will automatically extract the authors (`auth_group`,
`auth_n`, `authors`), and the associated almetric score (`altmetric`).
However, this functionality has been made optional as it can extend the
run time of the function (particularly in the case of a large number of
authors). It should be also noted that crossref tends to record
authorship less well (compared to PubMed).

``` r
# Example output from user_roles_n()
out_doi <- extract_doi(out_pubmed$doi,
                       get_auth = TRUE, get_almetric = FALSE, get_impact = FALSE)
```

<div style="border: 1px solid #ddd; padding: 5px; overflow-x: scroll; width:1000; ">
<table class="table table-striped" style="width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
doi
</th>
<th style="text-align:left;">
author\_group
</th>
<th style="text-align:left;">
title
</th>
<th style="text-align:right;">
year
</th>
<th style="text-align:left;">
journal\_abbr
</th>
<th style="text-align:left;">
volume
</th>
<th style="text-align:left;">
issue
</th>
<th style="text-align:left;">
pages
</th>
<th style="text-align:right;">
cite\_cr
</th>
<th style="text-align:right;">
auth\_n
</th>
<th style="text-align:left;">
author
</th>
<th style="text-align:left;">
journal\_full
</th>
<th style="text-align:left;">
journal\_issn
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
10.1002/bjs5.86
</td>
<td style="text-align:left;">
STARSurg Collaborative
</td>
<td style="text-align:left;min-width: 6in; ">
Prognostic model to predict postoperative acute kidney injury in
patients undergoing major gastrointestinal surgery based on a national
prospective observational cohort study
</td>
<td style="text-align:right;">
2018
</td>
<td style="text-align:left;">
BJS Open
</td>
<td style="text-align:left;">
2
</td>
<td style="text-align:left;">
6
</td>
<td style="text-align:left;">
400-410
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;min-width: 6in; ">
NA…
</td>
<td style="text-align:left;">
BJS Open
</td>
<td style="text-align:left;">
2474-9842
</td>
</tr>
<tr>
<td style="text-align:left;">
10.1136/bmjopen-2015-009812
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;min-width: 6in; ">
Outcomes After Kidney injury in Surgery (OAKS): protocol for a
multicentre, observational cohort study of acute kidney injury following
major gastrointestinal and liver surgery
</td>
<td style="text-align:right;">
2016
</td>
<td style="text-align:left;">
BMJ Open
</td>
<td style="text-align:left;">
6
</td>
<td style="text-align:left;">
1
</td>
<td style="text-align:left;">
e009812
</td>
<td style="text-align:right;">
7
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;min-width: 6in; ">
NA…
</td>
<td style="text-align:left;">
BMJ Open
</td>
<td style="text-align:left;">
2044-6055
</td>
</tr>
<tr>
<td style="text-align:left;">
10.1136/bmjopen-2015-008811
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;min-width: 6in; ">
Determining Surgical Complications in the Overweight (DISCOVER): a
multicentre observational cohort study to evaluate the role of obesity
as a risk factor for postoperative complications in general surgery
</td>
<td style="text-align:right;">
2015
</td>
<td style="text-align:left;">
BMJ Open
</td>
<td style="text-align:left;">
5
</td>
<td style="text-align:left;">
7
</td>
<td style="text-align:left;">
e008811
</td>
<td style="text-align:right;">
9
</td>
<td style="text-align:right;">
11
</td>
<td style="text-align:left;min-width: 6in; ">
Nepogodiev D, Chapman SJ, Glasbey J, Kelly M, Khat…
</td>
<td style="text-align:left;">
BMJ Open
</td>
<td style="text-align:left;">
2044-6055
</td>
</tr>
</tbody>
</table>
</div>
 

**2. `cite_publication()`**
---------------------------

The `cite_publication()` function will accept direct input from both
`extract_pmid()` and `extract_doi()`, however will also accept other
dataframes with the prerequiste columns. The columns can be specified
within the function. Other features include:

-   Highlighting any missing data essential for citation (e.g. author,
    jounral, etc). The issue, pmid, and doi are considered optional
    (depending on whether the dataset was generated from
    `extract_pmid()` or `extract_doi()`).

-   Automatically displaying all authors, however the auth\_max can be
    set from 1 to n to add “et al.” for any authors beyond that number.

-   The format can be customised via `cite_format` to match preferred
    referencing style (default is as shown below - Vancouver). Note the
    variable names in the string must exactly match an essential column
    (e.g. “author” not “Author” or “AUTHOR”)

``` r
  out_doi %>%
  # If a single-authorship collaborative publication (e.g. "STARSurg Collaborative") then display that
  dplyr::mutate(author = ifelse(is.na(author_group)==TRUE, author, author_group)) %>%
  cite_publication(journal = "journal_full", max_auth = 10,
                   cite_format = "author. title. journal. year; volume (issue): pages. PMID: pmid. DOI: doi.") %>%
  dplyr::mutate(citation = gsub("\\]", "", gsub("\\[", "", as.character(citation)))) %>%
  dplyr::select(citation) %>%
  knitr::kable(format="html") %>% kableExtra::kable_styling(bootstrap_options = "striped", full_width = F)
```

<table class="table table-striped" style="width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
citation
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
STARSurg Collaborative. Prognostic model to predict postoperative acute
kidney injury in patients undergoing major gastrointestinal surgery
based on a national prospective observational cohort study. BJS Open.
2018; 2 (6): 400-410. DOI:
<a href="http://dx.doi.org/10.1002/bjs5.86" class="uri">http://dx.doi.org/10.1002/bjs5.86</a>.
</td>
</tr>
<tr>
<td style="text-align:left;">
Incomplete citation data: author.
</td>
</tr>
<tr>
<td style="text-align:left;">
Nepogodiev D, Chapman SJ, Glasbey J, Kelly M, Khatri C, Drake TM, Kong
CY, Mitchell H, Harrison EM, Fitzgerald JE, et al. Determining Surgical
Complications in the Overweight (DISCOVER): a multicentre observational
cohort study to evaluate the role of obesity as a risk factor for
postoperative complications in general surgery. BMJ Open. 2015; 5 (7):
e008811. DOI:
<a href="http://dx.doi.org/10.1136/bmjopen-2015-008811" class="uri">http://dx.doi.org/10.1136/bmjopen-2015-008811</a>.
</td>
</tr>
</tbody>
</table>
