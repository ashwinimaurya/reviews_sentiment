# reviews_sentiment
Using Langchain and LLM to extract contextual reviews 

With plenty of customer reviews about business, it can be both a challenge and opprtunity for businesses to quickly understand customer sentiments. One such examples that is quite apparent in our daily life 
is when we search for restaurants and wanted to do quick google reviews to see its popularity, and red flags etc. When it comes to businesses, its is very important to quickly understand if any negatuve reviews of 
customers recently and address those. While we often see many businesses manually reploy to hundred of customers, it can be handful of task when it comes to chains such as Albertsons, or popular restaurants such as 
Texas Roadhouse etc. However this can be simplied with help of LLMs by using tools such as langchain. 

#### Analysing the customer reviews
Lets consider extracting the contextual keyword, a short summary and a possible business response to each review. Here we would like the business's response to reflect the customer's review sentiment and use a respectful tone. This can be set by clever prompting when call the response using LLM Api calls.

Lets consider the following reviews:

> 1. review_text_1="""The Texas Roadhouse is impressing me that the charcoal aroma is 100% injecting to the steak. The atmosphere is truly like living in Texas State.
I have to admit it is worth to try it when you are visiting in Bay Area!"""

> 2. review_text_2="""I visited the restaurant for the first time a week ago and I must say it was a very positive experience. The food we ordered was appetizing, the ribs didn't fall off the bone but they were flavorful, slightly charred, but very delicious. The BBQ Chicken was juicy, soft and very yummy, something I would definitely order again. The steak my father had was very tender and homecut, as he liked it very much. The staff was super friendly as our waitress approached us with enthusiasm and was open to any questions on the menu. The overall ambiente was inviting and quite like one would imagine a steakhouse to look like. Our overall conclusion would be to definitely come back when we're in Hayward, to enjoy a very pleasant food experience once again."""

```ruby
import pandas as pd
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```

Also, LLMs can help to answer the contextual infortaion such as ingredients in some item upto great extent. 

question='can you plz find me ingredients for items in triple quotes """poppi ginger lime prebiotic soda""" '

