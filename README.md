# Applied Data Analysis Project — Interactive Website

This repository contains the interactive website developed for the course  
**EPFL — Applied Data Analysis (CS-401)**.

Live website: https://ada-svelte.vercel.app/  
Course website: https://epfl-ada.github.io/teaching/fall2025/cs401/  

---

## Project Overview

As part of the Applied Data Analysis course, students are required to conduct a full data science project: from data collection to analysis, visualization, and communication.

This website presents our project in an interactive and accessible format, showcasing:
- The **research question**
- The **data collection and preprocessing pipeline**
- The **exploratory data analysis (EDA)**
- The **statistical and/or machine learning methods**
- The **key findings and insights**

The goal is to communicate results clearly and reproducibly, following best practices in data storytelling.

---

## About the Course

The Applied Data Analysis (CS-401) course focuses on the full data science pipeline, including:
- Data acquisition and cleaning  
- Statistical analysis and inference  
- Machine learning (supervised & unsupervised)  
- Data visualization and communication  

Students work in teams on a semester-long project using real-world datasets.

---

## Website Features

This project is implemented as an interactive web application using **Svelte** and deployed on **Vercel**.

Key features:
- Interactive visualizations  
- Clear narrative structure for data storytelling  
- Reproducible insights from the analysis  
- Fast and modern frontend framework  

---

## Tech Stack

- **Framework:** Svelte / SvelteKit  
- **Visualization:** D3.js / Plotly
- **Deployment:** Vercel  
- **Data processing:** Python (pandas, numpy, scikit-learn, etc.)  

---

## Repository Structure
```bash
ada-svelte/
├── src/ # Svelte application source code
├── static/ # Static assets
├── data/ # Processed datasets
├── package.json # Project dependencies
└── README.md
```


---

## Getting Started

To run the project locally:

```bash
# Clone the repository
git clone https://github.com/coralieb7/ada-svelte.git

# Navigate into the project
cd ada-svelte

# Install dependencies
npm install

# Run development server
npm run dev
```
Then open:
http://localhost:5173/
