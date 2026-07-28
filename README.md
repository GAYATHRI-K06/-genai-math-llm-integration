## Implementation of OpenAI Function Calling for Retrieving Current Stock Prices
**AIM:**

To develop a Python program using OpenAI Function Calling to retrieve the current stock price of a specified company by invoking a predefined function and displaying the result in JSON format.

## PROBLEM STATEMENT:
## DESIGN STEPS:
**STEP 1:**
Import the required modules (json) and define a function named get_stock_price() to return stock details.

**STEP 2:**
Define the function schema with the function name, description, and required parameter (company).

**STEP 3:**
Invoke the function using the company name, process the returned JSON data, and display the stock price information.
## PROGRAM:
````
import os
import openai
from dotenv import load_dotenv, find_dotenv
_ = load_dotenv(find_dotenv()) # read local .env file
openai.api_key = os.environ['OPENAI_API_KEY']
import json
````
````
def get_stock_price(company):
    """Get the current stock price of a company"""
    stock_info = {
        "company": company,
        "price": "198.45",
        "currency": "USD"
    }
    return json.dumps(stock_info)
````
````
functions = [
    {
        "name": "get_stock_price",
        "description": "Get the current stock price of a company",
        "parameters": {
            "type": "object",
            "properties": {
                "company": {
                    "type": "string",
                    "description": "The name of the company, e.g. Apple, Tesla, Microsoft"
                }
            },
            "required": ["company"],
        },
    }
]
````

```
messages=[
    {
        "role":"user",
        "content":"Get the stock price of tesla"
    }
]
```
```
# Call the ChatCompletion endpoint
response = openai.ChatCompletion.create(
   
    model="gpt-3.5-turbo",
    messages=messages,
    functions=functions
)
```
````
print(response)
response_message = response["choices"][0]["message"]
response_message
response_message["content"]
response_message["function_call"]
````
## OUTPUT:
<img width="722" height="727" alt="image" src="https://github.com/user-attachments/assets/5e179d72-ef72-4bb6-93d3-76ebdf4e7f6f" />
<img width="465" height="227" alt="image" src="https://github.com/user-attachments/assets/995f9d2f-647d-4bd2-a342-2329a1371394" />
<img width="570" height="120" alt="image" src="https://github.com/user-attachments/assets/57ead08e-5eff-4976-bd7d-ec63e0d63c5a" />



## RESULT:
Thus, the program to retrieve the current stock price of a company using OpenAI Function Calling was implemented successfully, and the stock information was displayed in JSON format.
