# Reviews Sentiment Analysis
Using Langchain and LLM to extract contextual reviews 

With plenty of customer reviews about business, it can be both a challenge and opprtunity for businesses to quickly understand customer sentiments. One such examples that is quite apparent in our daily life 
is when we search for restaurants and wanted to do quick google reviews to see its popularity, and red flags etc. When it comes to businesses, its is very important to quickly understand if any negatuve reviews of 
customers recently and address those. While we often see many businesses manually reploy to hundred of customers, it can be handful of task when it comes to chains such as Albertsons, or popular restaurants such as 
Texas Roadhouse etc. However this can be simplied with help of LLMs by using tools such as langchain. 

### Analysing the customer reviews
Lets consider extracting the contextual keyword, a short summary and a possible business response to each review. Here we would like the business's response to reflect the customer's review sentiment and use a respectful tone. This can be set by clever prompting when call the response using LLM Api calls.

Lets consider the following reviews:

> 1. review_text_1="""The Texas Roadhouse is impressing me that the charcoal aroma is 100% injecting to the steak. The atmosphere is truly like living in Texas State.
I have to admit it is worth to try it when you are visiting in Bay Area!"""

> 2. review_text_2="""I visited the restaurant for the first time a week ago and I must say it was a very positive experience. The food we ordered was appetizing, the ribs didn't fall off the bone but they were flavorful, slightly charred, but very delicious. The BBQ Chicken was juicy, soft and very yummy, something I would definitely order again. The steak my father had was very tender and homecut, as he liked it very much. The staff was super friendly as our waitress approached us with enthusiasm and was open to any questions on the menu. The overall ambiente was inviting and quite like one would imagine a steakhouse to look like. Our overall conclusion would be to definitely come back when we're in Hayward, to enjoy a very pleasant food experience once again."""

```ruby
import openai, os, pandas as pd
from dotenv import load_dotenv, find_dotenv
from langchain.prompts import ChatPromptTemplate
import json
import time

import pandas as pd
pd.set_option('display.max_rows', 500)
pd.set_option('display.max_columns', 500)
pd.set_option('display.width', 1000)
pd.set_option('max_colwidth', 1000)


_=load_dotenv(find_dotenv())
openai.api_key = os.environ['OPENAI_API_KEY']

llm_model_3 = "gpt-3.5-turbo"    
llm_model_4='gpt-4'    


def get_response_details(customer_review, model):
    
    from langchain.chat_models import ChatOpenAI
    
    review_template = """For the following text, extract the following information and output as python dictionary:

                        kwd:              Summarize the customer review with top keywords that express customer sentiment and \
                                          useful improving the customer experience and business operations.

                        summary_review:   Summarize the review in 1 sentence, max 20 words.

                        biz_response:     Write a appropriate response to the customer review, in american english and \
                                          respectful tone.


                        text: {text}

                        """
        
    prompt = ChatPromptTemplate.from_template(template=review_template)
    
    messages = prompt.format_messages(text=customer_review)
    
    chat_model= ChatOpenAI(temperature=0.2, model=model)
    
    response = chat_model(messages)

    return response.content


def get_product_template(product, model):
    
    from langchain.chat_models import ChatOpenAI
    
    review_template = """Take a deep breath. For the following product, extract the following information and output as python dictionary:

                        kwd:              List the top ingredients used to make this product.

                        nutritions:       List the top nutritions found in this product.

                        text: {product}

                        """
        
    prompt = ChatPromptTemplate.from_template(template=review_template)
    
    messages = prompt.format_messages(product=product)
    
    chat_model= ChatOpenAI(temperature=0.2, model=model)
    
    response = chat_model(messages)

    return response.content

def get_formatted_response(res):
    return json.loads(res)
```

Also, LLMs can help to answer the contextual infortaion such as ingredients in some item upto great extent. 

question='can you plz find me ingredients for items in triple quotes """poppi ginger lime prebiotic soda""" '

