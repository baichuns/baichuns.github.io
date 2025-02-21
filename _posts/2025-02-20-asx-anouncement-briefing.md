---
title: "Building an ai semi-agent for summarizing ASX daily announcements"
date: 2025-02-20 00:00:00 +0800
categories: ai agent, LLM
published: True
tags: [ai, agent, LLM, asx, summary, briefing]
---



Tracking company announcements on the **Australian Stock Exchange (ASX)** can provide valuable insights for investors, analysts, and financial professionals. Ideally, an **AI agent** could automatically scrape ASX’s ["Today's Announcements"](https://www.asx.com.au/markets/trade-our-cash-market/todays-announcements) page, download the relevant PDFs, and generate a summary report.  

## **The Challenge: Downloading Announcement PDFs**  
While the idea of a fully automated AI agent sounds great, there’s a **major roadblock**—extracting announcement PDFs directly from the ASX website.  

### **Challenges**  
- **🔄 Redirects & Validation:** PDF links on the ASX site **redirect** users to another page, often requiring additional interactions before downloading.  
- **🔐 Identity Verification:** Some downloads may require authentication, making it **hard to automate** through traditional web scraping techniques.  
- **📜 Dynamic Web Elements:** The announcement page is structured in a way that complicates **direct link extraction** for automated scripts.  

## **A Hybrid Approach**  
Instead of building a **fully automated** AI agent, a **semi-automated workflow** works best:  

1. **📥 Manually download** the announcements you’re interested in and store them in a local folder.  
2. **🤖 Use an AI-powered script** to process these PDFs, extract relevant insights, and generate a structured summary report.  
3. **🔧 Optionally, refine this pipeline** over time, incorporating **OCR or advanced scraping techniques** if the ASX website structure changes.  

## **Current Implementation**  
With this approach, our AI agent efficiently:  
✅ Reads **multiple ASX announcement PDFs** from a designated folder  
✅ Extracts **key insights** (e.g., sentiment, events, financial updates)  
✅ Generates **a structured summary report**  

While not fully autonomous, this method **balances automation with practicality**, allowing users to achieve time saving, focus on what matters—**analyzing insights instead of wrestling reading full report.**  It is a work in progress to achieve a fully automated agent.

 
## **Implementing the AI-Powered ASX Summary Tool**  

In this example, I use **Python, LangChain, OpenAI, and Gradio**. The following script processes ASX announcements, extracts summary using **GPT-4o-mini**, and uses interface via **Gradio**.  

### **📝 Code Example **  

```python
import gradio as gr
from pypdf import PdfReader
from langchain_community.chat_models import ChatOpenAI
from langchain.prompts import PromptTemplate


llm = ChatOpenAI(temperature=0.5, model="gpt-4o-mini")

# Define a prompt template to format the extracted content for AI analysis
prompt_template = PromptTemplate(
    input_variables=["content"],
    template=""" 
You are an assistant to help analyze Australian Stock Exchange (ASX) market company announcements,
The company announcement is : {content}
Please summarize the key insights!
[Summary of key information]  
"""
)

def generate_asx_summary():
    pdf_files = [f in os.listdir(announcement_dir) if f.endswith(".pdf")]

    all_summaries = []

    for pdf_path in pdf_files:
        reader = PdfReader(pdf_path)
        this_content = ""

        for page in reader.pages:
            this_content += page.extract_text() or ""

        formatted_prompt = prompt_template.format(content=this_content)
        response = llm.invoke(formatted_prompt)
        all_summaries.append(formatted_summary)

    return "## ASX Announcements Summary\n\n" + "\n\n---\n\n".join(all_summaries)

with gr.Blocks() as app:
    gr.Markdown("# ASX Market Announcements Summary")
    generate_button = gr.Button("Show Today's ASX Summary")
    output_text = gr.Markdown()
    generate_button.click(generate_asx_summary, inputs=[], outputs=[output_text])

app.launch()
```


# Interface Example

![](gif/asx1.png)