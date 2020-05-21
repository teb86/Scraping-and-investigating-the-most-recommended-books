# The most-recommended-books
This projet aims at building a DataFrame containing the books recommended by world-class people. 
## Packages:
* pandas 
* numpy 
* Requests 
* json
* bs4 BeautifulSoup 
* urllib parse
* re
* time
* matplotlib.pyplot 
* seaborn 
* textwrap
## Steps:
### 1. Gathering data:
First, I used this website **www.mostrecommendedbooks.com** to get the titles (and the authors) of the recommended books. I used the BeautifulSoup library to retrieve the data and add it to a dictionary.
Then, I converted the dictionary to a pandas dataframe that I stored in a csv file named **most_recommended.csv**.
After that, I used Google Books API to get additional information regarding the books we have. 
### Merging the datasets:
Since the titles in the two DFs are slightly different in terms of punctuation and short vs. long titles, and we don't have a numeric key (ISBN or ID) in the two DFs,  I merged these DFs on the indexes. To do this, I needed to harmonize the indexes by removing from the first DF all the books not found via Google Books API (books in the second DF) and appending them later after the join is made.
### Cleaning:
- Creating a column with the number of recommendations for each book
- Removing brackets and  quotes from 'category' column values
- Keeping only the year of publuication in the 'publication_date'
- Converting 'pages' to int datatype
### Storing:
The cleaned dataset was stored in a csv file named **books_clean.csv**.
### Analyzing:
4 questions were vizually answered using matplotlib and seaborn libraries:
- What are the most recommended books among the most recommended books?
- What are the most frequent categories in our recommenders list?
- What are the top 5 books in each category?
- What are the most recommended authors?
