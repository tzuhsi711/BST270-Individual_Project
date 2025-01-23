# BST270 Individual Project

This repository contains my attempt to reproduce tables/figures from FiveThirtyEight's [The Media Frenzy Around Biden Is Fadingy](https://fivethirtyeight.com/features/the-media-frenzy-around-biden-is-fading/).

## Environment

This project is implemented using the R programming language. The R environment and package management are handled through CRAN, ensuring compatibility with various versions of R.

## Project Structure

### Code Directory:

A complete code reproduction attempt is available at `./code/Biden_Media_2020.Rmd`. This Rmarkdown notebook can be compiled using RStudio into several formats including HTML and PDF. Compiled versions are stored in the `./document` directory.

### Document Directory:

Compiled versions of the document are stored as `./document/Biden_Media_2020.html` and `./document/Biden_Media_2020.pdf`.

### Data Directory:

Images of the original figure and table referenced in the analysis are provided in the `./data` directory for comparison.

All data files used in the analysis are available on [GitHub](https://github.com/fivethirtyeight/data/tree/master/hate-crimes) and are stored in the `./data` directory.

The following commands can also be utilised to obtain the data via command lines:

#### Cable News Data:

-   `cable_weekly.csv`: Weekly data on cable news mentions.

```{bash}
curl -o data/cable_weekly.csv https://raw.githubusercontent.com/fivethirtyeight/data/refs/heads/master/media-mentions-2020/cable_weekly.csv
```

#### Online News Data:

-   `online_weekly.csv`: Weekly data on online news mentions.

```{bash}
curl -o data/online_weekly.csv https://raw.githubusercontent.com/fivethirtyeight/data/refs/heads/master/media-mentions-2020/online_weekly.csv
```

### Getting Started

1.  Clone the GitHub repository.
2.  Open the Biden_Media_2020.Rmd file in R Studio (pre-requisite: install `dplyr`, `lubridate`, `tidyr`,`ggplot2`, and `knitr` R packages).
3.  Click "Preview" or "Run" to execute the notebook.

## Data

### Cable News

`cable_weekly.csv` contains the mentions of currently declared [major candidates](https://fivethirtyeight.com/features/heres-how-were-defining-a-major-presidential-candidate/) for the 2020 Democratic primary since December 30, 2018 across CNN, Fox News, and MSNBC. The TV News Archive measures coverage by splitting daily news footage into 15-second clips and finding the clips that contain a mention of our search query. Our search queries are the full names of each candidate. All candidates are queried starting December 30, 2018, however candidates are removed from the query once they have dropped out from the race.

| Column                       | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|------------------|------------------------------------------------------|
| `date`                       | Start date for the week of coverage. A week of coverage spans from Sunday through Saturday. The cutoff for measuring coverage for any given day is midnight Eastern Standard Time. (Clock changes for Daylight Saving Time are ignored.)                                                                                                                                                                                                                                                                                            |
| `name`                       | Candidate's name                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `matched_clips`              | Number of 15-second clips that match `query`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `all_candidate_clips`        | Number of 15-second clips that match the following query `("Amy Klobuchar" OR "Andrew Yang" OR "Bernie Sanders" OR "Beto O'Rourke" OR "Bill de Blasio" OR "Cory Booker" OR "Elizabeth Warren" OR "Eric Swalwell" OR "Jay Inslee" OR "Joe Biden" OR "John Delaney" OR "John Hickenlooper" OR "Julian Castro" OR "Julián Castro" OR "Kamala Harris" OR "Kirsten Gillibrand" OR "Marianne Williamson" OR "Michael Bennet" OR "Mike Gravel" OR "Pete Buttigieg" OR "Seth Moulton" OR "Steve Bullock" OR "Tim Ryan" OR "Tulsi Gabbard")` |
| `total_clips`                | Total number of 15-second clips that week across the three networks                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `pct_of_all_candidate_clips` | (`matched_clips` / `all_candidate_clips`)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `query`                      | Query for the GDELT Television API                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

Data is collected using the [GDELT Television API](https://blog.gdeltproject.org/gdelt-2-0-television-api-debuts/), which processes the data from the [TV News Archive](https://archive.org/details/tv).

### Online News

`online_weekly.csv` contains the mentions of currently declared [major candidates](https://fivethirtyeight.com/features/heres-how-were-defining-a-major-presidential-candidate/) for the 2020 Democratic primary since December 30, 2018 across in online news stories from two collections in the [Media Cloud](https://mediacloud.org/) database ([U.S. Top Online News](https://sources.mediacloud.org/#/collections/58722749) and [U.S. Top Digital Native News](https://sources.mediacloud.org/#/collections/57078150)). All candidates are queried starting December 30, 2018, however candidates are removed from the query once they have dropped out from the race.

| Column                         | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|------------------|------------------------------------------------------|
| `date`                         | Start date for the week of coverage. A week of coverage spans from Sunday through Saturday.                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `name`                         | Candidate's name                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `matched_stories`              | Number of stories that match `query`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `all_candidate_stories`        | Number of stories that match the following query `("Amy Klobuchar" OR "Andrew Yang" OR "Bernie Sanders" OR "Beto O'Rourke" OR "Bill de Blasio" OR "Cory Booker" OR "Elizabeth Warren" OR "Eric Swalwell" OR "Jay Inslee" OR "Joe Biden" OR "John Delaney" OR "John Hickenlooper" OR "Julian Castro" OR "Julián Castro" OR "Kamala Harris" OR "Kirsten Gillibrand" OR "Marianne Williamson" OR "Michael Bennet" OR "Mike Gravel" OR "Pete Buttigieg" OR "Seth Moulton" OR "Steve Bullock" OR "Tim Ryan" OR "Tulsi Gabbard")` |
| `pct_of_all_candidate_stories` | (`matched_stories` / `all_candidate_stories`)                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `query`                        | Query for Media Cloud                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
