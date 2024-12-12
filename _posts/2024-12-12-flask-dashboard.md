---
title: "Geoscience app demo using flask and voila"
date: 2024-11-11 00:00:00 +0800
tags: [dashboard, flask, voila]
---

# Introduction

This blog demonstrates a straightforward way to visualize a basic workflow function. The visualization is designed to be as simple as possible while remaining compatible for integration with other applications. Here, I present two approaches to achieve the visualization.

This application is a simple yet functional tool designed for the testing and trial phases of modulus application development. Modulus application development refers to the process of creating modular and scalable software components that can be integrated into larger systems. This approach emphasizes flexibility, reusability, and iterative development, making it well-suited for applications in fields like geospatial data processing and geophysics.

# Workflow visulisation using Flask

This simple web application provides an intuitive interface designed to visualize and process input data with ease. It offers the following features:

1. **Data Visualization**: 
   - The webapp allows users to upload and view their data in a clear and interactive format. 
   - This enables users to explore the detailed characteristics and insights within the dataset.

2. **Data Processing**:
   - Users can process the input data to achieve the desired height for upward continuation.
   - The tool simplifies complex calculations, ensuring accurate and efficient processing.

3. **Integrated Documentation**:
   - The webapp includes a dedicated **README page**, providing comprehensive documentation on the workflow.
   - This page guides users through each step, explaining the methodology and functionality of the application.

This web application is developed based on Python Flask, making it a lightweight yet powerful example of a simple app. While it serves as a standalone solution for specific tasks like upward continuation and data visualization, it can also be easily integrated into larger data analytics suites. Such integration allows it to function as an essential component within a broader ecosystem, streamlining workflows and enhancing data processing capabilities.

With its user-friendly design and integrated features, this web application serves as a valuable tool for handling and analyzing data in a streamlined manner. 

![uc_flask](gif/uc_flask.gif)


# Dashboard using voila
An alternative approach to showcasing the same functionality is by using **Voilà**, a tool that transforms Jupyter notebooks into standalone web applications. With Voilà, the same example can be quickly demonstrated in the form of an interactive dashboard. This allows users to take advantage of Jupyter's rich ecosystem for data analysis and visualization while presenting the results through a clean, user-friendly interface.

A quick demonstration of this example implemented via Voilà can provide an equally effective solution for visualization and interactivity. It highlights how the same underlying workflow can be adapted for different platforms to suit varied user preferences and project requirements.

With its user-friendly design and integrated features, this web application serves as a valuable tool for handling and analyzing data in a streamlined manner. It is particularly useful for tasks requiring upward continuation and detailed data exploration.


![voila dashboard](gif/voila_db.gif)

Streamlit is another option that I may consider incorporating into the demo at a later stage.