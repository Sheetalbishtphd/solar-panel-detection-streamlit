# Deployment Guide for Streamlit Cloud

## 🔐 Securing API Keys

All API keys have been removed from the code and are now managed through environment variables.

## 📝 Setup Instructions

### For Local Development

1. **Create a `.env` file** in the project root:
   ```bash
   cp env.example .env
   ```

2. **Add your API keys** to the `.env` file:
   ```
   ROBOFLOW_API_KEY=your_actual_roboflow_api_key
   GOOGLE_API_KEY=your_actual_google_api_key
   ROBOFLOW_PROJECT=solarpv-india-lczsp
   ROBOFLOW_WORKSPACE=
   ```

3. **Create `.streamlit/secrets.toml`** for Streamlit:
   ```bash
   cp .streamlit/secrets.toml.example .streamlit/secrets.toml
   ```

4. **Add your API keys** to `.streamlit/secrets.toml`:
   ```toml
   ROBOFLOW_API_KEY = "your_actual_roboflow_api_key"
   GOOGLE_API_KEY = "your_actual_google_api_key"
   ROBOFLOW_PROJECT = "solarpv-india-lczsp"
   ROBOFLOW_WORKSPACE = ""
   ```

5. **Install dependencies**:
   ```bash
   conda activate ann
   pip install -r requirements.txt
   ```

6. **Run the Streamlit app**:
   ```bash
   streamlit run streamlit_roboflow_7.py
   ```

### For Streamlit Cloud Deployment

1. **Push your code to GitHub** (without API keys)

2. **Go to Streamlit Cloud**: https://streamlit.io/cloud

3. **Deploy your app**:
   - Click "New app"
   - Select your GitHub repository: `Sheetalbishtphd/solar-panel-detection-streamlit`
   - Branch: `main`
   - Main file: `streamlit_roboflow_7.py`

4. **Add Secrets in Streamlit Cloud**:
   - Go to your app dashboard
   - Click on "⋮" (three dots menu)
   - Select "Settings" → "Secrets"
   - Add your secrets in TOML format:
   ```toml
   ROBOFLOW_API_KEY = "your_actual_roboflow_api_key"
   GOOGLE_API_KEY = "your_actual_google_api_key"
   ```
   - Click "Save"

5. **Deploy!** Your app will automatically redeploy with the secrets.

## 🚀 Running Python Scripts

For the command-line scripts (`yolo8_solar.py`, `yolo8_solar_csv.py`, `yolo8_solar_zoom21.py`):

1. **Create a `.env` file** (see above)

2. **Run the scripts**:
   ```bash
   conda activate ann
   python yolo8_solar.py
   python yolo8_solar_csv.py
   python yolo8_solar_zoom21.py
   ```

## 📁 Files Structure

```
solar_roboflow/
├── streamlit_roboflow_7.py       # Streamlit app (uses st.secrets or env vars)
├── yolo8_solar.py                # Excel input (uses env vars)
├── yolo8_solar_csv.py            # CSV input (uses env vars)
├── yolo8_solar_zoom21.py         # Zoom 21 version (uses env vars)
├── requirements.txt              # Updated with python-dotenv
├── env.example                   # Template for .env file
├── .streamlit/
│   └── secrets.toml.example      # Template for secrets.toml
├── .env                          # YOUR API KEYS (DO NOT COMMIT!)
├── .gitignore                    # Excludes .env and secrets.toml
└── DEPLOYMENT.md                 # This file
```

## ⚠️ Important Security Notes

- **NEVER** commit `.env` or `.streamlit/secrets.toml` to git
- **ALWAYS** use example files (`.example`) for templates
- The `.gitignore` file is configured to exclude sensitive files
- Verify your API keys are not visible in git before pushing

## 🔑 Where to Get API Keys

### Roboflow API Key
1. Go to: https://app.roboflow.com/
2. Login and navigate to Settings → Roboflow API
3. Copy your API key

### Google Maps API Key
1. Go to: https://console.cloud.google.com/
2. Create a project or select existing one
3. Enable "Maps Static API"
4. Go to Credentials → Create Credentials → API Key
5. Copy your API key
6. (Optional) Restrict the key to Maps Static API only

## 📧 Support

For issues or questions, contact the project maintainer.

