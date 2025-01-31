# wikihowAPI_pk

wikihowAPI_pk is basically base on [vigilant-umbrella/wikiHowUnofficialAPI
](https://github.com/vigilant-umbrella/wikiHowUnofficialAPI.git) but add more parser on it.

## New features

- [x] Return map(json) format for server use
- [x] Video Parser in Method section: each method is either one picture or video
- [x] Ingredients parser
- [x] Video Parser in section: some page would have videos after method section
- [x] Parse the search page of wikihow
- [ ] Parer to show more tipps

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

### Parse for wiki search page

```python
import wikihowunofficialapi as wha
how_tos: list = wha.search_wikihow_link("housing bubble")
return JsonResponse({"results": how_tos})
```

Output:

```json
{
  "results": [
    {
      "url": "https://www.wikihow.com/Make-Bubble-Solution",
      "img_url": "https://www.wikihow.com/images/thumb/8/8b/Make-Bubble-Solution-Step-10-Version-9.jpg/-crop-250-145-250px-Make-Bubble-Solution-Step-10-Version-9.jpg",
      "title": "How to Make a Homemade Bubble Mixture (With and Without Glycerin)",
      "update": "Updated 5 months ago",
      "views": "1,692,651 views",
      "sp_verif": "Quality Tested"
    },
    {
      "url": "https://www.wikihow.com/Take-a-Bubble-Bath",
      "img_url": "https://www.wikihow.com/images/thumb/0/0b/Take-a-Bubble-Bath-Step-8.jpg/-crop-250-145-193px-Take-a-Bubble-Bath-Step-8.jpg",
      "title": "How to Take a Bubble Bath",
      "update": "Updated 3 months ago",
      "views": "63,888 views",
      "sp_verif": ""
    }
  ]
}
```

### Json as ouput

The fields in map are basically the same as [Article Details](#article-details)

```python
import wikihowunofficialapi as wha

article = wha.Article('https://www.wikihow.com/Train-a-Dog')
article_json :Map = article.get()
```

Output:

```json
{
  "url": "https://www.wikihow.com/Make-Homemade-Spaghetti-Sauce",
  "title": "How to Make Homemade Spaghetti Sauce",
  "intro": "If you want to control the flavors and ingredients in spaghetti sauce, create your own! For a quick tomato and olive oil sauce that tastes fresh, simmer canned tomatoes in garlic, olive oil, and fresh basil. You can also make a meat spaghetti sauce that uses classic herbs and cooks until the meat is tender. Marinara sauce is also easy to make at a moment's notice. Just sauté a little onion and garlic in olive oil before you add red wine and tomatoes. Then cook the sauce until the tomatoes soften and lose their shape.",
  "ingredients": [
    {
      "recipe_name": "Quick Tomato and Olive Oil Sauce",
      "recipe_stuff": [
        "\n6 cloves garlic",
        "\n8 tablespoons (120 ml) extra-virgin olive oil, divided",
        "\n1 28-ounce (794 g) can of whole plum tomatoes packed in tomato juice",
        "\nSalt and pepper to taste",
        "\n10 basil leaves"
      ]
    }
  ],
  "n_methods": 3,
  "methods": [
    {
      "method_number": 1,
      "title": "Quick Tomato and Olive Oil Sauce",
      "steps": [
        {
          "number": 1,
          "title": "Crush 6 cloves of garlic",
          "description": "Peel 6 cloves of garlic and set them on a cutting board. Use the flat blade of a chef's knife to press down firmly on each clove of garlic.\nThe pressure will crush the garlic and release flavor.",
          "picture": "https://www.wikihow.com/images/thumb/a/aa/Make-Homemade-Spaghetti-Sauce-Step-1-Version-6.jpg/v4-460px-Make-Homemade-Spaghetti-Sauce-Step-1-Version-6.jpg"
        },
        {
          "number": 2,
          "title": "Sauté the garlic in olive oil for 2 to 3 minutes.",
          "description": "Put the crushed garlic into a non-reactive saucepan and pour in 5 tablespoons (74 ml) of the extra-virgin olive oil. Turn the burner to medium and heat the garlic until it becomes golden brown.\nStir the garlic occasionally so it cooks evenly.",
          "picture": "https://www.wikihow.com/video/c/cd/Make Homemade Spaghetti Sauce Step 2 Version 5.360p.mp4"
        }
      ]
    },
    {
      "method_number": 2,
      "title": "Classic Spaghetti Sauce with Meat",
      "steps": [
        {
          "number": 1,
          "title": "Cook the ground beef, onion, and garlic over medium heat for 7 to 8 minutes.",
          "description": "Pour 2 tablespoons (30 ml) of olive oil into a large skillet or Dutch oven and turn the burner to medium. Stir in 1 pound (450 g) of lean ground beef, 1 cup (150 g) of diced yellow onion, and 2 teaspoons (6 g) of minced garlic. Stir and cook the meat mixture until the beef is browned and crumbly.\nSince you're using lean ground beef, there shouldn't be much grease to drain off. If the meat is very greasy, drain off excess grease before finishing the sauce.",
          "picture": "https://www.wikihow.com/video/3/30/Make Homemade Spaghetti Sauce Step 8 Version 5.360p.mp4"
        },
        {
          "number": 2,
          "title": "Add the tomato paste, basil, oregano, thyme, fennel, and optional crushed pepper.",
          "description": "Scoop 6 ounces (170 g) of tomato paste into the skillet and add the herbs. Stir well to combine the ingredients and cook the sauce over medium heat for 1 to 2 minutes. Add salt and pepper to taste.",
          "picture": "https://www.wikihow.com/video/0/00/Make Homemade Spaghetti Sauce Step 9 Version 5.360p.mp4"
        }
      ]
    }
  ],
  "video": "https://www.youtube.com/embed/r1maSAsVGaY?enablejsapi=1",
  "num_votes": 11,
  "percent_helpful": 84,
  "is_expert": true,
  "last_updated": "2023-01-17T00:00:00",
  "views": 1360757,
  "co_authors": 56,
  "references": 18,
  "summary": "To make classic homemade spaghetti sauce with meat, start by browning the ground beef, onion, and garlic over medium heat for 7-8 minutes. Next, add the tomato paste and spices and cook the sauce for 2 minutes. Then, add the crushed tomatoes, broth, and sugar and simmer the sauce for 30 minutes. Remove the sauce from heat, spoon it over cooked pasta, and enjoy! For tips on making a quick marinara sauce, read on!",
  "warnings": [],
  "tips": [
    "Try doubling or tripling a batch of spaghetti sauce. Store it in an airtight container and freeze it for up to 6 months.\n"
  ]
}
```

## Credit

Most of the codes are base on [vigilant-umbrella/wikiHowUnofficialAPI
](https://github.com/vigilant-umbrella/wikiHowUnofficialAPI.git)
