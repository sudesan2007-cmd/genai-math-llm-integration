## Integration of a Mathematical Calulations with a Chat Completion System using LLM Function-Calling

### AIM:
To design and implement a Python function for calculating the volume of a cylinder, integrate it with a chat completion system utilizing the function-calling feature of a large language model (LLM).

### PROBLEM STATEMENT:
Design and implement a system where a user can input dimensions of a cylinder (radius and height),
and the system calculates its volume by invoking a Python function using the function-calling capabilities of an LLM.


### DESIGN STEPS:

#### STEP 1: Import necessary libraries, including OpenAI for LLM integration and math for mathematical operations.

#### STEP 2: Define a Python function to calculate the volume of a cylinder based on its radius and height.

#### STEP 3: Integrate the function into an LLM-based chat completion system with function-calling capabilities.

### PROGRAM:

```import os
import openai
import json
import math
from dotenv import load_dotenv, find_dotenv

# Load API Key
_ = load_dotenv(find_dotenv())
openai.api_key = os.environ["OPENAI_API_KEY"]

# Function to calculate area of a circle
def calculate_circle_area(radius):
    area = math.pi * radius * radius
    return json.dumps({
        "radius": radius,
        "area": round(area, 2)
    })

# Function definition
functions = [
    {
        "name": "calculate_circle_area",
        "description": "Calculate the area of a circle given its radius",
        "parameters": {
            "type": "object",
            "properties": {
                "radius": {
                    "type": "number",
                    "description": "The radius of the circle"
                }
            },
            "required": ["radius"]
        }
    }
]

# User message
messages = [
    {
        "role": "user",
        "content": "What is the area of a circle with radius 7?"
    }
]

# Call ChatCompletion
response = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=messages,
    functions=functions
)

response_message = response["choices"][0]["message"]

# Execute function if called
if response_message.get("function_call"):

    args = json.loads(response_message["function_call"]["arguments"])

    result = calculate_circle_area(args["radius"])

    print("Function Arguments:", args)
    print("Function Result:", result)

else:
    print(response_message["content"])
```


### OUTPUT:
<img width="551" height="102" alt="Screenshot 2026-10-27 162212" src="https://github.com/user-attachments/assets/ce2f301a-35fd-4c66-a6f0-43c4faa3f4e6" />



### RESULT:
Hence,the python program to design and implement a Python function for calculating the volume of a cylinder, integrating it with a chat completion system utilizing the function-calling feature of a large language model (LLM) is written successfully and executed.
