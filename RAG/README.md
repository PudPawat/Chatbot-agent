# RAG Chatbot Web App

This project is a simple web-based chatbot using Python (FastAPI) for the backend and Vue.js + Vuetify for the frontend. The backend connects to the OpenAI API to generate responses.

---

## Project Structure

```
RAG/
  backend/    # FastAPI backend (Python)
  frontend/   # Vue.js + Vuetify frontend
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
   - Create a `.env` file in the `backend` folder:
     ```sh
     echo "OPENAI_API_KEY=your_openai_api_key_here" > .env
     ```
   - Replace `your_openai_api_key_here` with your actual OpenAI API key.
4. **Run the FastAPI server:**
   ```sh
   uvicorn main:app --reload
   ```
   - The backend will be available at `http://localhost:8000`

---

## Frontend Setup (Vue.js + Vuetify)

1. **Navigate to frontend folder:**
   ```sh
   cd RAG/frontend
   ```
2. **Install dependencies:**
   ```sh
   npm install
   ```
3. **Run the development server:**
   ```sh
   npm run serve
   ```
   - The frontend will be available at `http://localhost:8080`

---

## Usage
- Open your browser and go to `http://localhost:8080`.
- Type a message in the chat box and interact with the OpenAI-powered chatbot!

---

## Deployment
- Push this project to GitHub as usual.
- For production deployment, consider environment variable management and CORS settings.

---

## License
MIT 