# Machine Learning Project Report - Book Recommendation System with Content-Based Filtering
## Project Overview
In this evolving digital era where access to various reading materials becomes easier, the development of book recommendation systems becomes increasingly important. 
These systems not only assist users in navigating through a vast number of available books but also enable them to discover reading materials that match their interests 
and preferences more efficiently. By providing personalized and relevant recommendations, book recommendation systems not only enhance users' reading experiences but also 
broaden the scope of literacy and knowledge within society as a whole. Research conducted by various institutions and publications has proven that the implementation of 
effective recommendation systems can boost book sales, increase user engagement, and promote diversity in reading. Therefore, this project has a significant impact on improving 
access to information, enhancing user satisfaction, and supporting the growth of the publishing industry and overall literacy in society.

**References**:
- Resnick, P., & Varian, H. R. (1997). Recommender systems. Communications of the ACM, 40(3), 56-58.
- Koren, Y., Bell, R., & Volinsky, C. (2009). Matrix factorization techniques for recommender systems. Computer, 42(8), 30-37.

## Business Understanding
### Problem Statements
- How can we help users find books that match their interests and preferences amidst the plethora of reading options available?
### Goals
- To develop an effective book recommendation system to assist users in finding reading materials that align with their interests and preferences more easily.
### Solution Statements
- Content-based filtering
  
This approach will utilize features of the books themselves, such as title, author, genre, and description, to create user and book profiles. The system will recommend books
that have similar features to books that the user has liked previously. For example, if a user likes books in the "science fiction" genre and by the author "Isaac Asimov",
the system will recommend books with similar genres and authors.

## Data Understanding
The data used in this project is the Books dataset obtained from Kaggle. The dataset contains 1000 rows of data records with no missing values. There are 10 columns in the dataset, 
namely index (which will be used as book_id) with integer data type, title with object data type, category with object data type, price with float data type, price after tax with 
float data type, tax amount with float data type, availability with integer data type, number of reviews with integer data type, book description with object data type, image link 
with object data type, and stars with integer data type.

Source: https://www.kaggle.com/datasets/jalota/books-dataset

### Descriptive Statistics of Data
|       |     book_id |      Price | Price_After_Tax | Tax_amount | Avilability | Number_of_reviews |       Stars |
|-------|------------:|-----------:|----------------:|-----------:|------------:|------------------:|------------:|
| count | 1000.000000 | 1000.00000 |      1000.00000 |     1000.0 | 1000.000000 |            1000.0 | 1000.000000 |
|  mean |  499.500000 |   35.07035 |        35.07035 |        0.0 |    8.585000 |               0.0 |    2.923000 |
|  std  |  288.819436 |   14.44669 |        14.44669 |        0.0 |    5.654622 |               0.0 |    1.434967 |
|  min  |    0.000000 |   10.00000 |        10.00000 |        0.0 |    1.000000 |               0.0 |    1.000000 |
|  25%  |  249.750000 |   22.10750 |        22.10750 |        0.0 |    3.000000 |               0.0 |    2.000000 |
|  50%  |  499.500000 |   35.98000 |        35.98000 |        0.0 |    7.000000 |               0.0 |    3.000000 |
|  75%  |  749.250000 |   47.45750 |        47.45750 |        0.0 |   14.000000 |               0.0 |    4.000000 |
|  max  |  999.000000 |   59.99000 |        59.99000 |        0.0 |   22.000000 |               0.0 |    5.000000 |

### Variables/Features in the Books Dataset are as follows:
- Title: book title.
- Category: book category.
- Price: book price.
- Price After tax: price of the book after tax.
- Tax amount: tax.
- Availability: available stock.
- Number of reviews: number of reviews.
- Book Description: book description.
- Image Link: link to view the book image.
- Stars: rating for each book with values ranging from 1 to 5 stars.

## Data Preparation
1. Handling Missing Values:

- Null or missing values can disrupt data consistency and accuracy. Therefore, it is important to handle null values properly to ensure data quality before modeling.
- In this project, the technique used to handle null values is to calculate null values for each column and then address these null values appropriately, such as through imputation or deletion of rows/columns.

2. Removing Duplicates (drop_duplicates):

- Data duplication can introduce bias in analysis and modeling. Therefore, duplicate removal steps are taken to ensure that each entity in the dataset is represented only once, resulting in more accurate and consistent analysis.
- In this project, the technique used is to use the drop_duplicates() method to remove rows with identical values for all columns.

3. Converting Data Series to List:
   
- In some cases, especially when working with certain methods or libraries that require input in the form of lists, converting data series to lists is necessary for proper data processing.
- In this project, the technique used is to use the tolist() method to convert data series into lists in certain columns such as book_id, title, and category.

4. Creating a New Dictionary and DataFrame:

- Creating a dictionary to determine key-value pairs in the data of book_id, title, and category allows for a more structured and easily manipulable representation. Additionally, converting the dictionary into a new dataframe facilitates data processing and prepares the data for modeling.
- In this project, the technique used is to create a dictionary from the data of book_id, title, and category, and then convert it into a new dataframe that will be used in modeling.

## Modeling
A recommendation system with content-based filtering is one approach in recommendation systems that utilizes intrinsic features of the recommended items to make recommendations to users. 
In the context of creating a book recommendation system, content-based filtering leverages book attributes such as title, author, genre, description, and other features to determine similarity 
between existing books and user preferences.

### Advantages of Content-Based Filtering
- High Personalization

Content-based filtering provides highly personalized recommendations because the recommendations are based on individual user preferences and characteristics of books that they have liked previously.
- No External User Data Required

This approach does not require information about other users, eliminating the need for external user data such as purchase history or user ratings.
- Adaptability to New Items

Content-based filtering can easily adapt to newly added items to the system since recommendations are based on intrinsic features of the items.
- Ability to Handle Long Tail

Content-based filtering is effective in handling the long tail, i.e., less popular or rarely searched items, because the system can recommend items based on feature similarity rather than popularity.

### Disadvantages of Content-Based Filtering
- Limitation in Discovering New Items

Content-based filtering tends to produce less diverse recommendations because it only recommends items that have similar features to items that the user has liked previously.
- Limitation in Handling Preference Changes

This approach is not effective in handling changes in user preferences because recommendations are solely based on features of previously liked books, without considering changes in user preferences.
- Dependence on Feature Extraction Quality

The quality of recommendations in content-based filtering depends heavily on the quality of feature extraction from books. If feature extraction is inaccurate, the resulting recommendations will also be inaccurate.
- Inability to Handle Filter Bubble

Content-based filtering tends to reinforce the filter bubble, where users only receive recommendations that align with their existing preferences, without being introduced to different content or diversifying their reading.

### Top-n Recommendation Test
|   |                                             title |              category |
|---|--------------------------------------------------:|----------------------:|
| 0 |                               While You Were Mine |    Historical Fiction |
| 1 |                             The House by the Lake |    Historical Fiction |
| 2 |                            Between Shades of Gray |    Historical Fiction |
| 3 |   World Without End (The Pillars of the Earth #2) |    Historical Fiction |
| 4 |                             Girl in the Blue Coat |    Historical Fiction |
| 5 |                                      Mrs. Houdini |    Historical Fiction |
| 6 | The Guernsey Literary and Potato Peel Pie Society |    Historical Fiction |
| 7 |           A Flight of Arrows (The Pathfinders #2) |    Historical Fiction |
| 8 |                                 The Secret Healer |    Historical Fiction |
| 9 |                         Girl With a Pearl Earring | Historical Fiction    |

## Evaluation
In this project, the evaluation metric used is precision. The "precision" evaluation metric in the context of recommendation systems measures how many recommended items are 
relevant to users' preferences or interests. In recommendation systems that use content-based filtering, precision provides insight into how well the system recommends books 
that align with users' preferred characteristics or content.

Precision measures the proportion of relevant items that are correctly predicted from all predicted items. In recommendation systems, this means calculating how many relevant 
books are recommended by the system compared to the total number of books recommended.

Here is the formula for Recommender System Precision.

$$Precision = \frac{number of recommendation that are relevant}{number of item recommended} x 100%$$

Where:
- number of recommendations that are relevant is the number of relevant items correctly predicted by the system.
- number of items recommended is the total number of recommended items.

In this project, the recommendation system is tested to provide the top 10 relevant book recommendations based on the input book. The results show that all recommended books 
are relevant/have the same category as the input book. Therefore, it can be said that the recommendation system in this project has a precision value of 100%. This is obtained 
from the calculation where the number of relevant recommendations is 10 and the number of recommendations is 10. Therefore, the precision value of the recommendation system created is 100%.

Based on this evaluation result, it can be concluded that the recommendation system can provide relevant book recommendations to help users explore and discover books that match 
their interests and preferences.
