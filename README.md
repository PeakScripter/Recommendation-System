# Book Recommendation-System

## Overview

This project implements a **Book Recommendation System** leveraging a dataset containing book details, user information, and ratings. The primary goal is to recommend books to users based on popularity or collaborative filtering methods. 

### Features:
1. **Data Preprocessing**:
   - Handled missing values in book attributes.
   - Filtered books and users based on specified thresholds for popularity and activity.

2. **Popular Book Recommendation**:
   - Identified the most popular books based on the number of ratings and their average rating.

3. **Collaborative Filtering**:
   - Built a user-book rating matrix for recommending books using collaborative filtering.

## Dataset

The project uses three datasets:
1. `Books.csv`: Contains details of books such as `ISBN`, `Book-Title`, `Book-Author`, `Year-Of-Publication`, and `Publisher`.
2. `Users.csv`: Contains user information including `User-ID` and demographics.
3. `Ratings.csv`: Includes user ratings for books in the format `User-ID`, `ISBN`, and `Book-Rating`.

### Dataset Preprocessing:
- Merged the datasets to align book details with user ratings.
- Dropped unnecessary or redundant columns.
- Filtered datasets to include:
  - Active users (users with more than 200 ratings).
  - Popular books (books with at least 50 ratings).

## Key Components

### 1. Popular Book Recommendation:
- Calculated:
  - **Number of Ratings**: Total number of ratings for each book.
  - **Average Rating**: Mean of ratings for each book.
- Sorted and displayed the top-rated books that are also frequently rated.

### 2. Collaborative Filtering:
- Created a **pivot table** with `Book-Title` as rows, `User-ID` as columns, and `Book-Rating` as values.
- This table serves as the basis for recommending books by identifying similar users or books.

### Code Highlights:
- **Merging Data**:
  ```python
  big = pd.merge(books, ratings, on='ISBN')
  ```
- **Filtering Popular Books**:
  ```python
  pop_df = pop_df[pop_df['num_ratings'] >= 250].sort_values('avg_ratings', ascending=False)
  ```
- **Building Pivot Table**:
  ```python
  chart = final_rating.pivot_table(index="Book-Title", columns="User-ID", values="Book-Rating")
  ```

## How to Use

1. **Environment Setup**:
   - Install Python (3.7+).
   - Install required libraries:
     ```bash
     pip install pandas numpy
     ```
   - Place the datasets (`Books.csv`, `Users.csv`, `Ratings.csv`) in the working directory.

2. **Run the Script**:
   Execute the Jupyter Notebook to generate recommendations.

3. **Outputs**:
   - Popular books ranked by the number of ratings and average rating.
   - Recommendations using collaborative filtering based on user preferences.

## Results

- **Popular Books**: Highlights books that are widely read and highly rated, such as:
  - *Harry Potter and the Sorcerer's Stone*.
  - *The Great Gatsby*.

- **Collaborative Recommendations**: Suggests books based on user activity and preferences.

## Limitations

1. Recommendations are based on explicit ratings only; implicit feedback is not considered.
2. Popularity-based recommendations might not capture user-specific interests.

## Future Enhancements

- Implement advanced collaborative filtering techniques (e.g., matrix factorization).
- Integrate content-based filtering to improve personalization.
- Deploy as a web application for broader usability.

## Acknowledgments

This project utilizes data from [Book-Crossing Dataset](http://www2.informatik.uni-freiburg.de/~cziegler/BX/).
