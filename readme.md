RealEstate-Chat (Raj AI by Magic Bricks)

Overview

This repository provides an AI-powered real estate chatbot, "Raj," designed to assist users in exploring and comparing residential properties in Bangalore. The chatbot leverages retrieval-augmented generation (RAG) and Azure OpenAI to answer user queries, provide property comparisons, and guide users through available listings in a conversational, professional, and engaging manner.

Features

- **Conversational Chatbot**: "Raj" interacts in Hinglish, collects user preferences, and provides concise, property-specific answers.
- **Property Comparison**: Lists and compares multiple properties based on user preferences (budget, BHK, amenities, etc.).
- **Data Pipeline**: Scrapes property details from MagicBricks, structures them, and feeds them to the chatbot.
- **Rich Responses**: Includes property images, links, and essential details in chat responses.
- **Extensible**: Easily add new property URLs and re-scrape data.

Directory Structure

```
magicbricks/
├── brochures/         # PDF brochures for reference (not used by code)
├── img/               # Property images (for reference)
├── output.txt         # JSON data of scraped property details (used by chatbot)
├── rag_chatbot.py     # Main Streamlit app for the chatbot
├── requirements.txt   # Python dependencies
├── scrape_urls.py     # Script to scrape property data from URLs
├── urls.txt           # List of property names and URLs to scrape
├── .devcontainer/     # Devcontainer config for VSCode/Codespaces
├── .gitignore         # Git ignore rules
```

How It Works

1. Data Collection

- **urls.txt**: Add or update property URLs here. Each line should have a property name and its MagicBricks URL.
- **scrape_urls.py**: Run this script to scrape property details (title, price, amenities, images, etc.) from the URLs in `urls.txt`. The results are saved in `output.txt`.

2. Chatbot Application

- **rag_chatbot.py**: The main Streamlit app. It loads `output.txt` and `urls.txt`, initializes the chatbot, and serves the web UI.
- The chatbot uses Azure OpenAI (GPT-4.1) to generate responses, referencing the property data.
- User preferences are collected interactively, and property options are presented in a concise, list-based format with images and links.

3. Brochures and Images

- **brochures/**: Contains PDF brochures for some properties. These are for user reference and are not used by the chatbot.
- **img/**: Contains property images, which may be referenced in the scraped data and shown in the chat UI.

Setup & Installation

Prerequisites

- Python 3.8+
- [Azure OpenAI Service](https://azure.microsoft.com/en-us/products/ai-services/openai-service/) (API key and deployment required)
- (Optional) Docker or VSCode Devcontainers for isolated development

1. Clone the Repository

```bash
git clone <repo-url>
cd magicbricks
```

2. Install Dependencies

```bash
pip install -r requirements.txt
```

3. Set Up Environment Variables

Create a `.env` file in the `magicbricks/` directory with the following variables:

```
AZURE_GPT41_URI=<your-azure-gpt4.1-endpoint>
AZURE_GPT41mini_URI=<your-azure-gpt4.1-mini-endpoint>
AZURE_OPENAI_API_KEY=<your-azure-openai-api-key>
AZURE_OPENAI_DEPLOYMENT=<your-deployment-name>
```

4. Scrape Property Data

Update `urls.txt` with your desired property URLs, then run:

```bash
python scrape_urls.py
```

This will generate/update `output.txt` with the latest property data.

5. Run the Chatbot

```bash
streamlit run rag_chatbot.py
```

The app will be available at [http://localhost:8501](http://localhost:8501).

(Optional) Using Devcontainers

If using VSCode or GitHub Codespaces, the `.devcontainer` setup will automatically install dependencies and launch the app.

Usage

- Open the web UI.
- Start chatting with "Raj" about your property preferences.
- Raj will ask for your requirements, compare properties, and provide links and images.
- For detailed property brochures, check the `brochures/` directory.

Customization

- **Add More Properties**: Add new lines to `urls.txt` and re-run `scrape_urls.py`.
- **Change Data Source**: Update the scraping logic in `scrape_urls.py` as needed.
- **Brochures/Images**: Add new brochures or images to their respective folders for reference.