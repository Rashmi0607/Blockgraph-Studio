# Blockgraph-Studio - VectorShift Pipeline Editor
A visual node-based pipeline editor built with React and FastAPI, similar to VectorShift's flow builder.

---

##  Live Demo : https://blockgraph-studio.netlify.app/

---
## Features

✅ **Node Abstraction System** - Reusable `BaseNode` component for easy node creation
✅ **7 Node Types** - Input, Output, Text, LLM, Transform, Filter, Aggregate
✅ **Dynamic Text Node** - Auto-resizing with `{{variable}}` detection and dynamic input handles
✅ **Modern Styling** - Clean UI with TailwindCSS and dark theme
✅ **Backend Integration** - FastAPI backend validates DAG structure
✅ **Visual Alerts** - User-friendly display of pipeline statistics

---

## 🖼️ Screenshots

🖼️ **Homepage Screenshot**
<img width="1920" height="903" alt="Img1" src="https://github.com/user-attachments/assets/d069d361-5e0b-41c8-86f0-53966ad37e8f" />

🖼️ **Project Details Screenshot**
<img width="1920" height="912" alt="Img2" src="https://github.com/user-attachments/assets/509517f5-7032-41e5-b6fa-1065ee38a753" />

---

## Project Structure

```
.
├── backend/          # FastAPI backend
│   ├── main.py      # API endpoints
│   └── requirements.txt
└── frontend/        # React frontend
    ├── src/
    │   ├── components/
    │   │   ├── nodes/        # Node components
    │   │   ├── PipelineCanvas.tsx
    │   │   └── Toolbar.tsx
    │   └── submit.js         # Backend API client
    └── package.json
```

## Setup & Run

### Backend

```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --reload
```

Backend runs at: `http://localhost:8000`

### Frontend

```bash
cd frontend
npm install
npm run dev
```

Frontend runs at: `http://localhost:8080`

## Usage

1. **Add Nodes** - Click node types in the toolbar to add them to the canvas
2. **Connect Nodes** - Drag from output handles to input handles to create connections
3. **Text Node Variables** - Type `{{variableName}}` in Text nodes to create dynamic input handles
4. **Submit Pipeline** - Click "Submit Pipeline" to validate and get statistics

The submit action will:
- Send nodes and edges to the backend
- Receive validation results (num_nodes, num_edges, is_dag)
- Display results in both a toast notification and browser alert

## API Endpoints

- `GET /` - Health check
- `POST /pipelines/parse` - Validate pipeline
  - Request: `{nodes: [], edges: []}`
  - Response: `{num_nodes: int, num_edges: int, is_dag: bool}`

## Architecture

### Node Abstraction
All nodes extend the `BaseNode` component which provides:
- Consistent styling and layout
- Dynamic input/output handles
- Icon and color customization

### DAG Validation
The backend uses depth-first search (DFS) with cycle detection to verify that the pipeline forms a valid Directed Acyclic Graph.

## Technologies

- **Frontend**: React, TypeScript, React Flow, TailwindCSS
- **Backend**: Python, FastAPI, Pydantic
- **Build**: Vite
