# VectorShift Pipeline Builder

This project is a **node-based pipeline builder** developed as part of the **VectorShift Frontend Technical Assessment**.  
It allows users to visually create pipelines using reusable nodes, submit the pipeline for analysis, and validate whether the pipeline forms a **Directed Acyclic Graph (DAG)**.

---

## 🚀 Overview

The VectorShift Pipeline Builder enables users to:
- Create pipelines using multiple node types
- Connect nodes visually
- Dynamically define variables in text nodes
- Submit the pipeline to a backend for structural analysis
- View pipeline statistics such as node count, edge count, and DAG validity

---

## 🧠 Key Features

### 1. Node Abstraction
- Implemented a reusable **BaseNode** component to eliminate duplicated code.
- Core nodes (Input, Output, Text, LLM) are built using this abstraction.
- Added multiple custom nodes such as **Calculator, Filter, Merge, Split, and Transform**.
- New nodes can be created easily by defining only configuration like title, handles, and content.

---

### 2. Unified Styling
- Applied consistent and modern styling across all nodes and UI components.
- Centralized styles make the UI clean and easy to maintain.

---

### 3. Enhanced Text Node
- Text node dynamically resizes as the user types.
- Supports variable placeholders using `{{variableName}}` syntax.
- Automatically creates input handles for detected variables.
- Handles are removed when variables are deleted.

---

### 4. Backend Integration & Pipeline Analysis
- Frontend sends pipeline nodes and edges to a FastAPI backend.
- Backend calculates:
  - Total number of nodes
  - Total number of edges
  - Whether the pipeline forms a Directed Acyclic Graph (DAG)
- Results are displayed in a user-friendly modal after submission.

---

## 🛠 Tech Stack

### Frontend
- React
- React Flow
- JavaScript
- CSS

### Backend
- Python
- FastAPI

---

## 📂 Project Structure
vectorshiftpipelinebuilder/
│
├── frontend/
│ ├── src/
│ │ ├── nodes/
│ │ │ ├── BaseNode.jsx
│ │ │ ├── InputNode.jsx
│ │ │ ├── OutputNode.jsx
│ │ │ ├── TextNode.jsx
│ │ │ ├── LLMNode.jsx
│ │ │ ├── CalculatorNode.jsx
│ │ │ ├── FilterNode.jsx
│ │ │ ├── MergeNode.jsx
│ │ │ ├── SplitNode.jsx
│ │ │ └── TransformNode.jsx
│ │ ├── submit.js
│ │ └── ...
│ └── package.json
│
├── backend/
│ ├── main.py
│ └── requirements.txt
│
├── README.md
└── TESTING_GUIDE.md


---


