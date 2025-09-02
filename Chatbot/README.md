# Chatbot with FastAPI & Streamlit

A simple chatbot application built with **FastAPI** for the backend and **Streamlit** for the frontend.  
The chatbot uses **Hugging Face Transformers** (TinyLlama) to generate text responses.  

---

## ✨ Features
- **FastAPI backend** serving a `/generate/text` endpoint for text generation.  
- **Streamlit frontend** with a chat interface (`st.chat_input` / `st.chat_message`).  
- **Hugging Face pipeline** using `TinyLlama/TinyLlama-1.1B-Chat-v1.0`.  
- **System prompt** ensures assistant always replies in Markdown.  
- **CUDA / CPU support** with `torch` for device detection.  

---

## 🧱 Project Structure
```
.
├── client.py        # Streamlit UI client
├── main.py          # FastAPI app with endpoints
├── model.py         # Model loading and text generation logic
├── requirements.txt # Dependencies
└── README.md        # Documentation
```

---

## 🖼️ How it Works
1. **Frontend** (`client.py`):  
   - Runs a Streamlit app.  
   - Maintains chat history in `st.session_state.messages`.  
   - Sends user prompts to FastAPI via `requests.get()`.  

2. **Backend** (`main.py`):  
   - Defines a `/generate/text` endpoint.  
   - Calls `load_text_model()` and `generate_text()` from `model.py`.  

3. **Model** (`model.py`):  
   - Loads `TinyLlama` with Hugging Face’s `pipeline`.  
   - Uses a system prompt that sets the chatbot persona.  
   - Generates text with sampling (`temperature`, `top_k`, `top_p`).  

---

## ✅ Prerequisites
- Python **3.10+**  
- [PyTorch](https://pytorch.org/get-started/locally/) (with CUDA if using GPU)  
- [Transformers](https://huggingface.co/docs/transformers) library  
- [FastAPI](https://fastapi.tiangolo.com/) and [Uvicorn](https://www.uvicorn.org/)  
- [Streamlit](https://streamlit.io/)  

---

## 🔧 Installation
1. Clone the repo:
   ```bash
   git clone <your-repo-url>
   cd <your-repo>
   ```

2. Create a virtual environment:
   ```bash
   python -m venv .venv
   source .venv/bin/activate   # On Windows: .venv\Scripts\activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

### Example `requirements.txt`
```txt
fastapi
uvicorn
torch
transformers
streamlit
requests
```

---

## ▶️ Running the Project
### Start the FastAPI backend
```bash
uvicorn main:app --reload --port 8000
```

### Start the Streamlit frontend
```bash
streamlit run client.py
```

Open your browser at:  
👉 [http://localhost:8501](http://localhost:8501) for the Streamlit UI.  
👉 [http://localhost:8000/docs](http://localhost:8000/docs) for FastAPI Swagger docs.  

---

## ⚙️ Configuration
- **Model**: Default is `TinyLlama/TinyLlama-1.1B-Chat-v1.0`.  
  Change inside `model.py` if you want another Hugging Face model.  

- **System Prompt** (in `model.py`):
  ```python
  system_prompt = '''
  Your name is FastAPI bot and you are a helpful
  chatbot responsible for teaching FastAPI to your users.
  Always respond in markdown.
  '''
  ```

- **Generation parameters** (in `generate_text`):
  ```python
  temperature=0.7
  max_new_tokens=256
  top_k=50
  top_p=0.95
  ```

---

## 🛠️ Improvements
- Add **streaming responses** with WebSockets instead of `requests.get`.  
- Cache the model (`load_text_model`) instead of reloading for each request.  
- Store chat history in a database (SQLite, Postgres, MongoDB).  
- Add **Dockerfile** for container deployment.  
- Deploy backend to **FastAPI on AWS/GCP/Azure** and frontend to **Streamlit Cloud**.  

---

## 📄 License
MIT (or your preferred license).  
