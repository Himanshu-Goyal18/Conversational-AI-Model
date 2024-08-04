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

## Requirements

* Python 3.x
* Jupyter notebook environment
* Hugging Face Transformers library
* IPython widgets library

## Code Structure

* `generate_text` function: generates output text based on user input
* `create_new_question_input` function: creates a new input area for user questions
* `output_area` widget: displays the generated output text

## Customization

* Adjust the `max_length` parameter in the `generate_text` function to change the maximum output length.
* Adjust the `temperature`, `top_k`, and `top_p` parameters in the `generate_text` function to change the output quality and coherence.

## License

This code is licensed under the MIT License.
