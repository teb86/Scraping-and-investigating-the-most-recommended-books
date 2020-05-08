# The most-recommended-books
This projet is about scraping data and building a dataset containing the books recommended by many world's famous personnalities with some general information regarding these books.
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
The first part of the gathering process was to scrap the titles (and the authors) of the books recommended. For this, the **www.mostrecommendedbooks.com** was used. In this website,  you can find a  long scrollable list of names, including Elon Musk, Steve Jobs, Malcolm Gladwell, Barrack Obama, etc. Clicking these names will redirect you to the reommender page where you can find all the books he/she recommended. So, first I  gathered all the recommender pages links in order to rotate over them and get the information needed. The links were added to a list named links[]. Then, I iterated over each link and craweled the title, the author and the recommender using the BeautifulSoup. The data was put in a nested dictionary 'books={}' where the names of the recommenders are the outer keys and the titles and authors are the inner keys.
After that, I converted the books dict to a pandas dataframe that I stored in a csv file **most_recommended.csv**.
The second part of the garthering was to use google books api to get additional information about the titles in the dataset I already had. Since I don't have the books IDs yet or the books ISBN, I used the title and author combination in the URL search params like this:
google_url = 'https://www.googleapis.com/books/v1/volumes?q=intitle:{}+inauthor:{}&country=MA'
By using the title and the author, I had to urllib.parse to encode non ASCII characters that can be found in an author name for example.
The data was put in a list and the result was 2909 books and 94 non found books.
### Merging the datasets:
First, I needed to remove from the first dataframe, which was scraped through the mostrecommendedbooks website, the books not found via google books api. Why? Since I didn't have a numeric primary key (ISBN or ID) in the two DF that would have certainly allowed a perfect merge, and the titles in the two DF are slightly different in terms of punctuation and smaller vs long title, I figured out that the best way to merge these DF is through the (similar) index. Then, after joing the two DF, I appended the not-found books.
### Cleaning:
- Creating a column with the number of recommendations for each book
- Removing brackets and  quotes from 'category' column values
- Keeping only the year of publuication in the 'publication_date'
- Converting 'pages' to int datatype
### Storing:
The merged and cleaned dataset was stored in a csv file named books_clean.csv
### Analyzing:
4 questions were vizually answered using matplotlib and seaborn libraries:
- What are the most recommended books among the most recommended books?
- What are the most frequent categories in our recommenders list?
- What are the top 5 books in each category?
- What are the most recommended authors?


