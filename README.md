# TMDB Movie Dashboard (Power BI)

This Power BI dashboard analyzes and visualizes data from two key sources:
- [TMDB 5000 Movies Dataset](https://www.kaggle.com/datasets/chaitanyasood1/tmdb-5000-movies?select=tmdb_5000_movies.csv)
- Oscar-winning movies dataset

The dashboard provides interactive insights into movie revenues, genres, popularity, and award winning movies, with additional custom logic and dynamic data transformations.

---

## Datasets Used

1. **tmdb_5000_movies.csv** – Kaggle dataset containing movie metadata from TMDB.
2. **Oscar Dataset** – Custom dataset listing Oscar-winning and nominated movies.

---

## Key Scenarios Implemented

### Scenario 1:
- Dashboard only includes movies that are **present in both the TMDB and Oscars datasets**.
- In the Oscars dataset, some movies appear multiple times due to re-releases. We are programmatically removing duplicate movie entries in the Oscar dataset, where some movies have been re-released (i.e., same movie title appears multiple times with different release years). 
- A **dynamic Power Query transformation** removes all but the **most recent release** of each duplicate title.
- This logic is dynamic and will auto-handle future changes or additions to the data.

### Scenario 2 (Bonus Page):
- A second page in the dashboard connects to `dog_types.xlsx` (a file listing dog types).
- It fetches **all subcategories of dog breeds** dynamically using this API:
  - [`https://dog.ceo/api/breeds/list/all`](https://dog.ceo/api/breeds/list/all)
- The Power Query logic is dynamic – any update in the source Excel will re-trigger the API pull and update the results.

---

## Dashboard Features

### Key KPIs
- Total Movies (Intersection of TMDB & Oscar datasets)
- Total Revenue
- Total Genres
- Total Votes

### Visuals
- **Slicer using Field Parameters**: Choose Top N category (Movies, Companies, etc.)
- **Stacked Column Chart**: Top N Production Companies by Revenue
- **Stacked Column Chart**: Top N Movies by Revenue
- **Stacked Bar Chart**: Total Revenue by Genre
- **Stacked Column Chart**: Most Voted Movies
- **Pie Chart**: Count of Movies by Language
- **Treemap**: Most Popular Movies by Popularity Score
- **Stacked Column Chart**: Top Budgeted Movies
- **Stacked Bar Chart**: Most Award-Winning Movies
- **Slicer Filters**:
  - Genre
  - Release Year

---

## Data Model Overview

The data model merges two primary datasets:

| Table Name           | Description                                         |
|----------------------|-----------------------------------------------------|
| `tmdb_5000_movies`   | Movie metadata including genres, ratings, etc.      |
| `oscar_movies`       | List of Oscar-nominated and awarded movies          |
| `merged_dataset`     | Final model with intersecting records + transformation logic |

Additional query: `dog_types.xlsx` + API connection for dog breed subcategories.

---

## Files in This Repository

| File Name               | Description                                 |
|--------------------------|---------------------------------------------|
| `TMDB_Dashboard.pbix`   | Power BI report file                        |
| `tmdb_5000_movies.csv`  | TMDB movies dataset (from Kaggle)           |
| `oscar_dataset.csv`     | Oscar-winning/nominated movies              |
| `dog_types.xlsx`        | Excel file for dog breed types              |
| `/screenshots/`         | Screenshots of report visuals               |
| `README.md`             | Project documentation                       |

---

## Dashboard Preview

![Main Dashboard](screenshots/tmdb_overview.png)
![Genre Analysis](screenshots/genre_analysis.png)

---

## How to Use

1. **Clone or download** this repository.
2. Open `TMDB_Dashboard.pbix` in **Power BI Desktop** (May 2024 or newer).
3. Go to **Transform Data** and update the file paths for:
   - `tmdb_5000_movies.csv`
   - `oscar_dataset.csv`
   - `dog_types.xlsx`
4. Refresh the report to view the latest insights and API data.

---

## Tools & Technologies

- Power BI Desktop
- Power Query (M language)
- DAX for KPIs and calculations
- External APIs (dog.ceo)
- Field Parameters for dynamic visual switching

---

## Notes

- The dataset and report are built for learning and demonstration purposes.
- The API integration for dog breeds demonstrates Power BI’s capability to connect external dynamic sources and merge them with local data.
- The `.pbix` file may exceed GitHub’s 100MB limit. If so, Git LFS (Large File Storage) is used.

---

## License

This project is intended for educational and non-commercial purposes. Data is sourced from publicly available datasets and APIs.

---

## Contributions

Suggestions and improvements are welcome! Fork the repo, make your changes, and submit a pull request.
