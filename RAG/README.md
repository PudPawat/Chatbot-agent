# Minimal ChatGPT-like Webapp

This project is a minimal chatbot webapp with a modern chat UI (like ChatGPT) and a FastAPI backend that connects to OpenAI's GPT API.

---

## Project Structure

```
RAG/
  backend/      # FastAPI backend (Python)
    main.py
    requirements.txt
    .env
  frontend/     # Vue 3 + Vite modern chat UI
    (Vite project files)
```

---

## Prerequisites
- Python 3.7+
- Node.js & npm
- OpenAI API key

---

## Backend Setup (FastAPI)

1. **Navigate to backend folder:**
   ```sh
   cd RAG/backend
   ```
2. **Install dependencies:**
   ```sh
   pip install -r requirements.txt
   ```
3. **Set up environment variables:**
   - Edit `.env` and add your OpenAI API key:
     ```sh
     OPENAI_API_KEY=your_openai_api_key_here
     ```
4. **Run the FastAPI server:**
   ```sh
   uvicorn main:app --reload
   ```
   - The backend will be available at `http://localhost:8000`

---

## Frontend Setup (Vue 3 + Vite)

1. **Navigate to RAG and create the frontend:**
   ```sh
   cd RAG
   npm create vite@latest frontend -- --template vue
   cd frontend
   npm install
   ```
2. **Replace `src/App.vue` with the provided minimal chat UI code.**
3. **Run the frontend:**
   ```sh
   npm run dev
   ```
   - The frontend will be available at `http://localhost:5173`

---

## Usage
- Open your browser and go to `http://localhost:5173`.
- Type a message and chat with the OpenAI-powered bot!

---

## License
MIT 