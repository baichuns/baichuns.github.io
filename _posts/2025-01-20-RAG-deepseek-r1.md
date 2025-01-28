---
title: "Building RAG Step-by-Step with DeepSeek-R1 and Ollama"
date: 2025-01-20 00:00:00 +0800
categories: LLM
tags: [LLM, deepseek, RAG]
---

---

## Preamble

This tutorial assumes familiarity with basic Python programming and access to the terminal. We'll integrate libraries for loading data, generating embeddings, and querying the model. Let’s dive in!

---

## What is RAG?

RAG stands for retrieval augmented generation. In simple terms, RAG is the process of providing a Large Language Model (LLM) with specific information relevant to the prompt.

## Why is RAG important?

Although LLMs are highly capable, their reasoning is limited to the data they were trained on. This limitation becomes evident when requesting information beyond their training data, such as proprietary data or recent common knowledge. RAG addresses this issue by retrieving relevant information for the prompt and providing it to the model as context.

## Guide to Setting Up and Running DeepSeek-R1 with Ollama

In this guide, we will walk through installing Ollama, starting the Llama server, and pulling and running the DeepSeek-R1 model for natural language querying with a simple Python script.


## Install Ollama

To install Ollama, simply run the following command in your terminal:

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

## Import all necessary libraries

```python
import os
from llama_index.core import SimpleDirectoryReader, Settings, VectorStoreIndex
from llama_index.embeddings.huggingface import HuggingFaceEmbedding
from llama_index.llms.ollama import Ollama
from llama_index.llms.openai import OpenAI
from llama_index.core.prompts import PromptTemplate
```

Note: You may need an OpenAI API key, even if not using OpenAI models
```python
os.environ["OPENAI_API_KEY"] = ""
```

## Load documents from the specified directory for embedding knowledge

```python
loader = SimpleDirectoryReader(
    input_dir="",
    required_exts=[".pdf"],
    recursive=True
)
docs = loader.load_data()
```

## Set the embedding model; we use a locally available HuggingFace model

```python
Settings.embed_model = HuggingFaceEmbedding(model_name="BAAI/bge-small-en-v1.5")
index = VectorStoreIndex.from_documents(docs)
```

## Function to load the appropriate LLM based on the model option

```python
load_llm = lambda get_model: Ollama(model="deepseek-r1:latest")
```

## Load the LLM

```python
llm = load_llm("DeepSeek-R1")
Settings.llm = llm
```

## Create the query engine

Query engine is a generic interface that allows you to ask question over your data.

A query engine processes a natural language query and provides a detailed response. Typically, it is constructed using one or more indexes through retrievers. By combining multiple query engines, you can achieve more sophisticated functionality.

```python
query_engine = index.as_query_engine()
```

## Define a QA prompt template

At its simplest, querying is just a prompt call to an LLM: it can be a question and get an answer, or a request for summarization, or a much more complex instruction.

More complex querying could involve repeated/chained prompt + LLM calls, or even a reasoning loop across multiple components.

Create a template for a question-and-answer (QA) prompt that will guide the model in generating responses. This template should include placeholders for context information and the user’s query, ensuring that the model can provide clear and concise answers based on the given context.

```python
qa_prompt_tmpl_str = (
    "Below is the context information. \n"
    "\n"
    "{context_str}\n"
    "\n"
    "Using the context provided, please think through each step to answer the query clearly. \n"
    "If you don't know the answer, simply state, 'I don't know.' \n"
    "Query: {query_str}\n"
    "Answer: "

)
qa_prompt_tmpl = PromptTemplate(qa_prompt_tmpl_str)
query_engine.update_prompts({"response_synthesizer:text_qa_template": qa_prompt_tmpl})
```

## Query the engine

```python
response = query_engine.query("What is <*>?")
print(response)
```

If you prefer, you can also create a user interface (UI) for your local output. This UI can help you visualize and interact with the results more easily, making it more user-friendly and accessible. By building a UI, you can customize the way data is presented and provide a more intuitive experience for users who may not be familiar with the underlying code or technical details.