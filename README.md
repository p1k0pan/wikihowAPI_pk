# wikihowAPI_pk

wikihowAPI_pk is basically base on [vigilant-umbrella/wikiHowUnofficialAPI
](https://github.com/vigilant-umbrella/wikiHowUnofficialAPI.git) but add more parser on it.

## New features

- [x] Return map(json) format for server use
- [x] Video Parser in Method section: each method is either one picture or video
- [x] Ingredients parser
- [ ] Video Parser in section: some page would have videos after method section
- [ ] Parer to show more tipps
- [ ] Make `<li>` inside a Text visible after parsing

## Installation

```bash
pip install wikiHowUnofficialAPI, wikihowAPI-pk
```

## Usage

### Random HowTo

Learn random stuff! Retuns a random WikiHow article URL.

```python
import wikihowunofficialapi as wha

ra = wha.random_article()
print(ra)
```

### Article Details

Uses the article URL to return various details about an article. In addition, it returns whether an article is written by an expert or not.

```python
import wikihowunofficialapi as wha

article = wha.Article('https://www.wikihow.com/Train-a-Dog')

print(article.url)					# Print Article's URL
print(article.title)					# Print Article's Title
print(article.intro)					# Print Article's Introduction
print(article.n_methods)				# Print number of methods in an Article
print(article.methods)					# Print a list of methods in an Article
print(article.num_votes)				# Print number of votes given to an Article
print(article.percent_helpful)				# Print percentage of helpful votes given to an Article
print(article.is_expert)				# Print True if the Article is written by an expert
print(article.last_updated)				# Print date when the Article was last updated
print(article.views)					# Print the number of views recieved by Article
print(article.co_authors)				# Print the number of co-authors of an Article
print(article.references)				# Print the number of references in an Article
print(article.summary)					# Print Article's summary
print(article.warnings)					# Print Article's warnings
print(article.tips)					# Print Article's tips

first_method = article.methods[0]
first_step = first_method.steps[0]
print(first_step)					# Print Article's first step of the first method
print(first_step.title)					# Print the title of Article's first step of the first method
print(first_step.description)				# Print the description of Article's first step of the first method
```

### Images

Retrieves a list of image included in a step as URLs.

```python
import wikihowunofficialapi as wha

article = wha.Article('https://www.wikihow.com/Train-a-Dog')
print(article.methods[0].steps[0].picture)		# Print the URL of the image of Article's first step of the first method

```

### Search

Searches WikiHow for the string and returns a list containing the title of the articles. The default max results is 10, but this can be changed.

```python
import wikihowunofficialapi as wha

max_results = 1
how_tos = wha.search_wikihow("sleep", max_results)
print(how_tos[0])
```

### Json as ouput

The fields in map are basically the same as [Article Details](#article-details)

```python
import wikihowunofficialapi as wha

article = wha.Article('https://www.wikihow.com/Train-a-Dog')
article_json :Map = article.get()
```

## Credit

Most of the codes are base on [vigilant-umbrella/wikiHowUnofficialAPI
](https://github.com/vigilant-umbrella/wikiHowUnofficialAPI.git)
