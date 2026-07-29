example ipython nb:
![Pasted image 20260117160755](Pasted%20Images/Pasted%20image%2020260117160755.png)

### If using Google Collab
- Store the Open Ai API Key in `Secrets` Section in Left pane of Google-Colab
```python
from google.colab import userdata
key=userdata.get('openai_key')
```

### Import Open-Ai

```python
#!pip install openai
!pip install openai==0.28.1
import openai
openai.api_key = key
```


### Access Generate-content  Method
- Follows 2 Parameters:
	- `question`
	- `model`
- We Format the message we want to send explaining who we are (user, assistant, admin) and the question as content
- We Use Chat Completion Method to receive a response
- Response we receive is assigned to a variable whose content is accessed

```python
def Generate_Content(question, model="gpt-3.5-turbo"):
    messages = [{"role": "user", "content": question}]
    openai_response = openai.ChatCompletion.create(
        model=model,
        messages=messages
    )
    return openai_response.choices[0].message["content"]
```


### We can Access the method `Generate_Content` and pass prompts to it
- We Write a prompt
- We save the response after calling the method after calling the method with prompt as argument
```python
prompt = f"""
Summarize Alice in the wonderland in 3 sentences
"""
response = Generate_Content(prompt)
print(response)

f=open('response.txt','w')
f.write(response)
f.close()
```










#cognizant #cognizant_course #GenAI #openAi #python