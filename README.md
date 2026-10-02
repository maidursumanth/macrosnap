# 🥗 MacroSnap
Live macrosnap : https://macrosnap-fj7gfkvoyq6scnhwlczbnu.streamlit.app/

### AI-Powered Meal & Nutrition Tracker

**MacroSnap** is an AI-powered nutrition tracking application that allows users to upload a photo of their meal and receive an AI-generated analysis of the meal, including estimated **calories and macronutrients**.

The application also allows users to receive their daily nutrition summary through **WhatsApp**, making it easier to track meals without manually entering every food item.

---

## 🚀 Features

* 📸 **Meal Image Analysis**

  * Upload a photo of your meal.
  * AI analyzes the food visible in the image.

* 🧠 **AI-Powered Nutrition Analysis**

  * Uses Google's Gemini API to analyze meal images.
  * Provides estimated calories and macronutrients.
  * Users can also ask nutrition-related questions through the chat interface.

* 💬 **AI Chat Interface**

  * Interactive chat-based nutrition assistant.
  * Supports both text and image inputs.

* 📊 **Macro & Calorie Tracking**

  * Provides estimated:

    * Calories
    * Protein
    * Carbohydrates
    * Fats

* 📱 **WhatsApp Nutrition Summary**

  * Generates a daily nutrition summary.
  * Sends the summary to the user's WhatsApp using Twilio.

* 👤 **Simple User Onboarding**

  * Users enter their name and WhatsApp number before using the application.

* 🌐 **Web-Based Interface**

  * Built with Streamlit for a simple and responsive user experience.

---

## 🛠️ Tech Stack

| Technology            | Purpose                                  |
| --------------------- | ---------------------------------------- |
| **Python**            | Core application development             |
| **Streamlit**         | Web application interface                |
| **Google Gemini API** | AI-powered meal and nutrition analysis   |
| **Google GenAI SDK**  | Gemini API integration                   |
| **Twilio**            | WhatsApp messaging                       |
| **TOML**              | Secure application secrets configuration |

---

## 🏗️ Architecture

```text
                    ┌─────────────────────┐
                    │       User          │
                    │                     │
                    │ Text / Meal Photo   │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │     Streamlit       │
                    │     Frontend        │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │    Gemini API       │
                    │                     │
                    │ Image + Text        │
                    │ Analysis             │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Nutrition Response  │
                    │                     │
                    │ Calories            │
                    │ Protein             │
                    │ Carbs               │
                    │ Fat                 │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │       Twilio        │
                    │      WhatsApp      │
                    └─────────────────────┘
```

---

## 📂 Project Structure

```text
macrosnap/
│
├── app.py
├── prompts.py
├── requirements.txt
│
├── .streamlit/
│   └── secrets.toml
│
└── README.md
```

### `app.py`

Contains the main Streamlit application, Gemini integration, chat functionality, image processing, and WhatsApp summary functionality.

### `prompts.py`

Contains the system prompts and predefined messages used to control the AI nutrition assistant.

### `requirements.txt`

Contains the Python dependencies required to run the application.

### `.streamlit/secrets.toml`

Stores API credentials and other sensitive configuration values.

> **Never commit `secrets.toml` or API keys to GitHub.**

---

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/maidursumanth/macrosnap.git
```

Navigate into the project:

```bash
cd macrosnap
```

---

### 2. Create a virtual environment

Windows:

```powershell
python -m venv venv
```

Activate it:

```powershell
venv\Scripts\activate
```

---

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

If you don't already have a `requirements.txt`, install:

```bash
pip install streamlit google-genai twilio
```

---

## 🔐 Environment Configuration

Create:

```text
.streamlit/secrets.toml
```

Add your credentials:

```toml
GEMINI_API_KEY = "your_gemini_api_key"

TWILIO_ACCOUNT_SID = "your_twilio_account_sid"
TWILIO_AUTH_TOKEN = "your_twilio_auth_token"
TWILIO_WHATSAPP_FROM = "whatsapp:+your_twilio_number"
TWILIO_CONTENT_SID = "your_twilio_content_sid"
```

### Security

Add this to `.gitignore`:

```gitignore
.streamlit/secrets.toml
venv/
__pycache__/
```

Never upload API keys, authentication tokens, or other credentials to GitHub.

---

## ▶️ Run the Application

Start Streamlit:

```bash
streamlit run app.py
```

The application will be available locally at:

```text
http://localhost:8501
```

---

## 💡 How It Works

### Step 1: User Onboarding

The user enters:

* Name
* WhatsApp number

The application creates a Gemini chat session for the user.

### Step 2: Upload a Meal

The user uploads a:

* JPG
* JPEG
* PNG

image of their meal.

### Step 3: AI Analysis

The application sends the image and prompt to Gemini.

Gemini analyzes the meal and generates nutritional information.

### Step 4: View Results

The AI response is displayed inside the Streamlit chat interface.

Users can continue asking questions about their meal.

### Step 5: WhatsApp Summary

The user can request a nutrition summary.

The application sends the generated summary through Twilio WhatsApp.

---

## 🧠 AI Integration

MacroSnap uses Google's Gemini API through the official Python GenAI SDK.

The application creates a Gemini client:

```python
from google import genai

gemini_client = genai.Client(
    api_key=GEMINI_API_KEY
)
```

A chat session is then created with a custom system instruction:

```python
st.session_state.chat = gemini_client.chats.create(
    model=MODEL_NAME,
    config=types.GenerateContentConfig(
        system_instruction=SYSTEM_PROMPT
    ),
)
```

This allows the application to maintain a conversational nutrition assistant rather than treating every request as an isolated query.

---

## 📱 WhatsApp Integration

MacroSnap uses **Twilio** to send nutrition summaries through WhatsApp.

The generated summary is cleaned and formatted before being sent using a Twilio content template.

```text
MacroSnap
   ↓
Generate daily summary
   ↓
Clean / format response
   ↓
Twilio API
   ↓
WhatsApp
   ↓
User
```

---

## ⚠️ Limitations

MacroSnap provides **AI-generated estimates**, not medically verified nutritional measurements.

The accuracy of the nutritional information can vary depending on:

* Image quality
* Food visibility
* Portion size
* Ingredients used
* Cooking method
* Similar-looking foods

For accurate dietary or medical decisions, users should consult a qualified nutrition or healthcare professional.

---

## 🔮 Future Improvements

Some potential improvements include:

* 📊 Daily and weekly nutrition dashboard
* 🎯 Personalized calorie and macro goals
* 🗄️ User database and meal history
* 📈 Nutrition progress charts
* 🔐 User authentication
* 🥘 Better portion-size estimation
* 🧾 Food and nutrition database integration
* 📱 Mobile-friendly interface
* 🔔 Automated daily WhatsApp reports
* 🏃 Personalized diet recommendations
* 💾 Persistent conversation and meal history
* ☁️ Production deployment and monitoring

---

## ☁️ Deployment

MacroSnap can be deployed using **Streamlit Community Cloud**.

Basic deployment flow:

```text
GitHub Repository
        ↓
Streamlit Community Cloud
        ↓
Install requirements.txt
        ↓
Configure Secrets
        ↓
Deploy
```

Make sure all required packages are present in `requirements.txt`:

```txt
streamlit
google-genai
twilio
```

API credentials should be configured through Streamlit's Secrets management rather than committed to the repository.

---

## 🎯 Project Goals

MacroSnap was built to explore how **Generative AI, computer vision, APIs, and web application development** can be combined to solve a practical everyday problem.

The project demonstrates:

* Python application development
* Streamlit application development
* Generative AI integration
* Multimodal AI
* API integration
* Prompt engineering
* Session-state management
* WhatsApp automation
* Cloud deployment
* Secure secret management

---

## 👨‍💻 Author

**Sumanth**

GitHub:
https://github.com/maidursumanth

---

## 📄 License

This project is available for educational and personal use.

---

### ⭐ If you find this project useful

Consider giving the repository a star ⭐ and exploring the source code.
