# Himanshu's AI: A Conversational AI Model

## Overview

Himanshu's AI is a conversational AI model built using the Hugging Face Transformers library. It uses the GPT-2 XL model to generate human-like responses to user input.

## Features

* User-friendly interface using Jupyter widgets
* Ability to ask questions and receive responses
* Support for multiple questions and responses
* Adjustable parameters for output quality and length

## Usage

1. Run the code in a Jupyter notebook environment.
2. Enter a question in the input text area.
3. Click the "Generate" button to receive a response.
4. Click the "Ask Another Question" button to ask another question.

## Code

### Importing Libraries

```python
from transformers import AutoTokenizer, AutoModelForCausalLM
import textwrap
import ipywidgets as widgets
from IPython.display import display, clear_output, HTML
```

### Loading Model and Tokenizer
```python
model_name = "gpt2-xl"
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForCausalLM.from_pretrained(model_name)
tokenizer.pad_token = tokenizer.eos_token
```
### Text Generation Function
```python
def generate_text(input_text):
    try:
        prompt_text = f"{input_text}\nAnswer the question without repeating the question above.\n"
        inputs = tokenizer(prompt_text, return_tensors="pt", padding=True, truncation=True)
        outputs = model.generate(
            inputs["input_ids"],
            attention_mask=inputs["attention_mask"],
            max_length=250,
            num_return_sequences=1,
            temperature=0.7,
            top_k=50,
            top_p=0.95,
            do_sample=True,
            pad_token_id=tokenizer.eos_token_id
        )
        generated_text = tokenizer.decode(outputs[0], skip_special_tokens=True)
        cleaned_generated_text = generated_text.replace(prompt_text, "").strip()
        wrapped_generated_text = textwrap.fill(cleaned_generated_text, width=100)
        output_area.value = wrapped_generated_text
    except Exception as e:
        output_area.value = f"Error during text generation: {str(e)}"
```
### Creating Input and Output Areas
```python
def create_new_question_input():
    global text_area, generate_button, continue_button
    clear_output(wait=True)
    display(HTML("""
    <style>
        .widget-container {
            margin-bottom: 20px;
            display: flex;
            flex-direction: column;
            width: 100%;
            flex-grow: 1;
        }
        .widget-textarea {
            font-size: 14px;
        }
        .widget-button {
            margin-top: 10px;
            width: 99%;
        }
    </style>
    """))
    text_area = widgets.Textarea(
        value='',
        placeholder='Enter your question here...',
        disabled=False,
        layout=widgets.Layout(width='99%', height='60px')
    )
    generate_button = widgets.Button(description='Generate', layout=widgets.Layout(width='99%'))
    generate_button.on_click(lambda b: generate_text(text_area.value))
    continue_button = widgets.Button(description='Ask Another Question', layout=widgets.Layout(width='99%'))
    continue_button.on_click(lambda b: create_new_question_input())
    output_area = widgets.Textarea(
        value='',
        placeholder='Output will be displayed here...',
        disabled=True,
        layout=widgets.Layout(width='99%', height='300px'),
        style={'overflow': 'hidden'}
    )
    display(widgets.HTML(value="<b>Ask Himanshu's AI anything:</b>"), text_area, generate_button, widgets.HTML(value="<b>Himanshu's AI response:</b>"), output_area, continue_button)
```
### Initial Display

```python
create_new_question_input()
```

## Evaluation

### Initial Interface

![Initial Interface](initial_screenshot.png)

### After Asking a Question

![After Asking a Question](after_asking_screenshot.png)






