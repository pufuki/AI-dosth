# MultiInfer

Beginner-friendly full-stack project that lets you try 8 AI features from a web app.

- **Frontend:** React
- **Backend:** FastAPI
- **AI Provider:** Hugging Face Inference API
- **No local GPU required**

This project is for learning and demonstration. You run the frontend and backend locally, and the backend calls Hugging Face models through an API key.

---

## What You Can Do

AI Studio includes these features:

1. Sentiment Analysis
2. Text Generation
3. Image Classification
4. Speech Recognition (audio to text)
5. Text Summarization
6. Named Entity Recognition (people, places, organizations, etc.)
7. Translation (English to French)
8. Question Answering (answer from context text)

---

## Project Structure

```text
ai-studio/
  backend/    # FastAPI server and AI API calls
  frontend/   # React user interface
```

---

## Prerequisites

Install these first:

- **Python 3.10+**
- **Node.js 18+**
- **npm** (comes with Node.js)
- A free **Hugging Face account**

Check versions:

```bash
python --version
node --version
npm --version
```

---

## Step 1: Create a Hugging Face API Key (Free)

1. Sign up: <https://huggingface.co/join>
2. Open token settings: <https://huggingface.co/settings/tokens>
3. Click **New token**
4. Give it a name (example: `ai-studio`)
5. Set role to **Read**
6. Create and copy the token (`hf_...`)

Keep this token private.

---

## Step 2: Run the Backend

Open terminal in your project root, then:

```bash
cd ai-studio/backend

python -m venv venv
source venv/bin/activate
# Windows (Command Prompt): venv\Scripts\activate
# Windows (PowerShell): .\venv\Scripts\Activate.ps1

pip install -r requirements.txt
cp .env.example .env
```

Now open `.env` and set:

```env
HF_API_KEY=hf_your_token_here
```

Start backend server:

```bash
uvicorn main:app --reload --port 8000
```

Backend URLs:

- API: <http://localhost:8000>
- Swagger docs: <http://localhost:8000/docs>

---

## Step 3: Run the Frontend

Open a **new terminal**:

```bash
cd ai-studio/frontend
npm install
npm start
```

Frontend URL:

- App: <http://localhost:3000>

---

## How to Test Quickly

After both servers are running:

1. Open <http://localhost:3000>
2. Pick a feature from the sidebar
3. Enter sample input
4. Submit and view results

You can also test backend endpoints directly in Swagger:
<http://localhost:8000/docs>

---

## API Endpoints

| Method | Endpoint | Purpose |
|---|---|---|
| GET | `/` | Health check |
| GET | `/models` | List model names |
| POST | `/sentiment` | Analyze sentiment |
| POST | `/generate` | Generate text |
| POST | `/classify-image` | Classify image file |
| POST | `/transcribe` | Transcribe audio file |
| POST | `/summarize` | Summarize text |
| POST | `/ner` | Extract entities |
| POST | `/translate` | Translate English to French |
| POST | `/qa` | Answer question from context |

---

## Common Problems and Fixes

### `HF_API_KEY not set`
- Make sure `.env` exists in `ai-studio/backend`
- Make sure it contains:
  `HF_API_KEY=hf_...`
- Restart backend after updating `.env`

### `503 Model is loading`
- This is normal on first request
- Wait 20–30 seconds and try again

### CORS error in browser
- Confirm backend is running on port `8000`
- Confirm frontend is running on port `3000`

### `npm install` fails
- Check Node.js version (`18+` recommended)
- Delete `node_modules` and retry:
  ```bash
  rm -rf node_modules package-lock.json
  npm install
  ```

### Audio transcription feels slow
- Large files take longer to process
- Try a shorter audio clip first

---

## Tech Stack

- React 18
- FastAPI
- httpx
- python-multipart
- Hugging Face Inference API

---

## Notes

- This project uses external inference APIs, so response time depends on network and model warm-up.
- Free-tier limits may apply on Hugging Face.
- Do not commit your `.env` file or API key.
