## Project Description
This repository contains a step-by-step implementation of a popularity-based movie recommendation baseline system built using Python and Pandas. The project demonstrates the full machine learning pipeline for recommendation systems, including data inspection, cleaning, user-item interaction matrix generation, sparsity calculation, baseline recommendation modeling, and output export.

## Objectives
- Perform data inspection and cleaning on raw rating interaction logs.
- Construct a User-Item Interaction Matrix to structure explicit rating data.
- Measure and explain dataset sparsity.
- Build a Non-Personalized Popularity-Based Recommender System using average ratings and interaction frequency thresholds.
- Export top recommendation baselines to CSV for downstream deployment.

## Dataset
The dataset `ratings.csv` represents user rating logs with the following columns:
- **`user_id`**: Unique string identifier for each user (e.g., `U001`).
- **`movie_id`**: Unique string identifier for each movie (e.g., `M001`).
- **`movie_title`**: Descriptive title of the movie (e.g., *Nairobi Nights*).
- **`rating`**: Explicit feedback score on a 1–5 scale.
- **`timestamp`**: ISO-8601 formatted timestamp recording when the rating occurred.

## Methodology
1. **Data Inspection**: Examined initial dataset structure (509 rows, 5 columns), column data types, missing values, and row duplicates.
2. **Data Cleaning**: 
   - Removed 3 exact duplicate rows.
   - Removed 3 records containing missing `user_id` or `movie_id` fields.
   - Identified and filtered out 3 invalid ratings outside the standard 1–5 scale (`-1`, `0`, `6`).
   - Resulted in a clean dataset of 500 valid ratings.
3. **Interaction Analysis**: Calculated interaction metrics across 50 unique users and 24 unique movies.
4. **User-Item Matrix**: Formed a $50 \\times 24$ interaction matrix where values correspond to explicit user ratings.
5. **Sparsity Calculation**: Calculated sparsity using the formula:
   $$\\text{Sparsity} = 1 - \\left( \\frac{\\text{Observed Ratings}}{\\text{Users} \\times \\text{Movies}} \\right)$$
   Achieved a matrix sparsity of **58.33%** (500 observed ratings / 1,200 total possible interactions).
6. **Popularity Recommendation**: Grouped data by movie, calculated average ratings and rating counts, applied a threshold of `rating_count >= 10`, and sorted by average rating (descending) and rating count (descending).

## Key Findings
- **Cleaned Dataset Size**: 500 records
- **Unique Users**: 50
- **Unique Movies**: 24
- **Overall Average Rating**: 3.45 / 5.00
- **Most Active User**: `U010` (17 ratings)
- **Most Rated Movie**: `M001` / *Nairobi Nights* (37 ratings)
- **Top Recommended Movie**: `M021` / *Market Day* (Average Rating: 4.47, Rating Count: 15)

## Limitations
1. **Lack of Personalization**: The model delivers identical recommendations to all users regardless of individual preferences or historical viewing habits.
2. **Popularity Bias**: Less-popular or niche items ("long-tail" catalog items) are systematically overlooked even if they closely align with specific user interests.
