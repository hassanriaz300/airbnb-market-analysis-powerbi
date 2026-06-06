# # Rental Market Insights Dashboard

A Power BI dashboard project analyzing public rental listing data across major cities.  
The dashboard focuses on market size, pricing, room types, host activity, superhost distribution, and guest rating performance.

![Dashboard Overview](screenshots/dashboard-overview.png)

---

## Project Overview

This project was created to practice Power BI dashboard design, DAX measures, interactive reporting, bookmarks, slicers, and visual storytelling.

The dashboard answers questions such as:

- Which cities have the highest number of listings?
- Which room types dominate the rental market?
- How does average price vary by city and room type?
- Which cities have the most hosts?
- How do ratings differ across cities?
- What share of listings are managed by superhosts?
- Which cities contribute most to the total market share?

---

## Dashboard Pages

### 1. Market Overview

The first page provides a high-level summary of the rental market.

Main visuals include:

- KPI cards for total listings, cities, hosts, average price, average rating, and property types
- Listings by city
- Listings by room type
- Average price by room type
- Average price by city
- Listings over the years
- Top 5 cities by total hosts
- Key insights section
- City slicer for interactive filtering

![Market Overview](screenshots/market-overview.png)

---

### 2. Ratings Analysis

The second page focuses on guest ratings and market share analysis.

Main visuals include:

- Cumulative market share by city
- Superhost vs non-superhost listings
- Rating score comparison by city
- Rating categories such as accuracy, cleanliness, location, and communication
- Bookmark navigation between overall and detailed views
- Key insight text explaining rating and market patterns

![Ratings Analysis](screenshots/ratings-analysis.png)

---

## Tools Used

- Power BI Desktop
- Power Query
- DAX
- Bookmarks
- Slicers
- Git
- GitHub

---

## Dataset

The project uses a public rental listings dataset based on Airbnb-style listing data.

Main fields used include:

- City
- Room type
- Price
- Host ID
- Host superhost status
- Review scores
- Availability
- Listing date/year
- Rating categories such as cleanliness, location, accuracy, and communication

---

## Key Features

### Interactive Slicer

A city slicer was added to allow users to filter the dashboard by city.

Slicer used:

- City slicer
- Dropdown style
- Applied across dashboard visuals

---

### Bookmarks

Bookmarks were used on the Ratings Analysis page to switch between different analysis views.

Bookmarks created:

- Overall
- Detailed

The bookmarks help users move between a summary-level view and a more detailed rating breakdown without creating too many separate pages.

---

### Navigation Buttons

Sidebar navigation buttons were added for:

- Market Overview
- Ratings Analysis

The buttons improve dashboard usability and make the report feel more like a professional business dashboard.

---

## DAX Measures

### Total Listings

```DAX
Total Listings = COUNTROWS(Listings)
```

### Total Cities

```DAX
Total Cities = DISTINCTCOUNT(Listings[city])
```

### Total Hosts

```DAX
Total Hosts = DISTINCTCOUNT(Listings[host_id])
```

### Total Property Types

```DAX
Total Types = DISTINCTCOUNT(Listings[property_type])
```

### Average Price

```DAX
Avg Price = AVERAGE(Listings[price])
```

### Clean Average Price

A cleaned average price measure was used to reduce the impact of extreme outliers.

```DAX
Avg Price Clean =
AVERAGEX(
    FILTER(
        Listings,
        Listings[price] > 0 &&
        Listings[price] <= 500
    ),
    Listings[price]
)
```

### Average Rating Out of 5

The rating column was stored on a 0–100 scale, so it was converted to a 0–5 scale.

```DAX
Avg Rating Out of 5 =
DIVIDE(
    AVERAGE(Listings[review_scores_rating]),
    20
)
```

### Total Superhost Listings

```DAX
Superhost Listings =
CALCULATE(
    [Total Listings],
    Listings[host_is_superhost] = "t"
)
```

### Total Non-Superhost Listings

```DAX
Non-Superhost Listings =
CALCULATE(
    [Total Listings],
    Listings[host_is_superhost] = "f"
)
```

### Superhost Share

```DAX
Superhost Share =
DIVIDE(
    [Superhost Listings],
    [Total Listings]
)
```

### Average Accuracy Rating

```DAX
Avg Accuracy =
AVERAGE(Listings[review_scores_accuracy])
```

### Average Cleanliness Rating

```DAX
Avg Cleanliness =
AVERAGE(Listings[review_scores_cleanliness])
```

### Average Location Rating

```DAX
Avg Location =
AVERAGE(Listings[review_scores_location])
```

### Average Communication Rating

```DAX
Avg Communication =
AVERAGE(Listings[review_scores_communication])
```

---

## Dashboard Design

The dashboard uses a clean BI-style layout with KPI cards, rounded containers, consistent spacing, and a limited color palette.

### Color Palette

| Purpose | Hex Code |
|---|---|
| Main Color | `#0F5C5C` |
| Secondary Color | `#16CBCB` |
| Page Background | `#F7F8FA` |
| Chart Teal | `#1B8A87` |
| Chart Coral Red | `#F45B69` |
| Chart Yellow | `#F6B82F` |
| Chart Green | `#79A95C` |
| Chart Purple | `#8C78B5` |

---

## Typography

The dashboard uses Segoe UI for a clean and readable Power BI design.

| Usage | Font Style |
|---|---|
| Section Titles | Segoe UI, 14 pt |
| Chart Titles / KPI Labels | Segoe UI, 12 pt |
| Body Text / Axis Labels | Segoe UI, 11 pt |
| Legends / Notes | Segoe UI, 9 pt |

---

## Key Insights

- Paris and New York have the highest number of listings.
- Entire place listings account for the largest share of the rental market.
- Hotel rooms show the highest average price per night.
- Superhost and non-superhost listings vary strongly across cities.
- Ratings are generally high across major cities, with small differences between cleanliness, location, communication, and accuracy.
- Market share is concentrated in a small number of major cities.

---

## Project Structure

```text
.
├── airbnb.pbip
├── airbnb.Report/
├── airbnb.SemanticModel/
├── data/
├── docs/
├── screenshots/
│   ├── dashboard-overview.png
│   ├── market-overview.png
│   └── ratings-analysis.png
└── README.md
```

---

## What I Learned

Through this project, I practiced:

- Creating Power BI KPI cards
- Building bar, column, donut, line, and matrix visuals
- Writing DAX measures
- Cleaning and formatting measures for dashboard use
- Creating slicers for interactivity
- Using bookmarks for report navigation
- Designing a consistent dashboard layout
- Using a color palette and typography system
- Preparing a Power BI project for GitHub

---

## Disclaimer

This project uses a public Airbnb-style listings dataset for educational and portfolio purposes only.  
It is not affiliated with, endorsed by, or sponsored by Airbnb.

The dashboard branding was changed to a generic rental market theme to avoid using official Airbnb branding or logos.
