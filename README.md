# Solar Bot 4.0 ☀️

> A smart AI-powered solar energy advisor that tells you exactly what solar system you need — just enter your location and electricity usage.

---

## About

Solar Bot 4.0 is a fast API backend that uses real weather data and AI to recommend the perfect solar panel setup for any location. It helps homeowners and businesses go solar without the confusion.

---

## What It Does

- Takes your **location** and **monthly electricity usage (kWh)** as input
- Fetches **live solar irradiance data** from Open-Meteo weather API
- Sends data to **Llama 3.3 70B** (via Groq) for AI analysis
- Returns a **structured JSON recommendation** that includes:
  - Recommended system size (kW)
  - Number of solar panels needed
  - Panel type suggestion
  - Estimated annual energy production
  - Battery storage recommendation
  - Backup power duration
  - System type (grid-tied / hybrid / off-grid)
  - How much of your electricity needs will be covered

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| **FastAPI** | Backend web framework |
| **Groq API** | AI inference (Llama 3.3 70B) |
| **Open-Meteo API** | Free weather & solar data |
| **Geopy** | Convert location name to coordinates |
| **Pydantic** | Input validation |
| **Uvicorn / Gunicorn** | ASGI server |
| **Vercel** | Deployment |

---

## API Endpoint

### `POST /ask`

**Request Body:**
```json
{
  "Location": "Lahore, Pakistan",
  "Electricity_KWH_per_month": 500
}
```

**Response:**
```json
{
  "response": "A 5 kW solar system is recommended for your location.",
  "json_list": [
    { "name": "recommended_system_size_kw", "short_description": "..." },
    { "name": "number_of_panels", "short_description": "..." },
    ...
  ],
  "detailed_summary": "...",
  "confidence_percent": 92,
  "timestamp": "2025-05-04T15:00:00Z"
}
```

---

## Getting Started

### 1. Clone the repo
```bash
git clone https://github.com/mohsin-khann/solar_bot4.0.git
cd solar_bot4.0
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Set up environment variables

Create a `.env` file in the root folder:
```env
GROQ_API_KEY=your_groq_api_key_here
```

Get your free Groq API key at: [https://console.groq.com](https://console.groq.com)

### 4. Run the server
```bash
uvicorn solar_api:app --reload
```

The API will be live at: `http://localhost:8000`

---

## Project Structure

```
solar_bot4.0/
├── solar_api.py          # Main API with structured JSON response
├── solarr_api2.py        # Alternate API version (text response)
├── solar_api3.py         # Additional API variant
├── solar_functions.py    # Fetches live solar & weather data
├── requirements.txt      # Python dependencies
├── vercel.json           # Vercel deployment config
└── .env                  # API keys (not committed)
```

---

## Deployment

This project is ready to deploy on **Vercel**. The `vercel.json` config is already included.

```bash
vercel deploy
```

---

## Environment Variables

| Variable | Description |
|----------|-------------|
| `GROQ_API_KEY` | Your Groq API key for LLM access |

---

## License

MIT License — free to use and modify.

---

Made with passion for clean energy by [Mohsin Khan](https://github.com/mohsin-khann)
