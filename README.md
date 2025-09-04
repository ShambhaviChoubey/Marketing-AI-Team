# AI Marketing Team - n8n Automation

## Overview

This project builds a powerful, all-in-one AI marketing team using no-code automation. The system is triggered via Telegram, allowing users to request a wide variety of marketing assets through simple text or voice messages. An intelligent AI agent then interprets the request and leverages specialized sub-workflows to generate content, including images, blog posts, LinkedIn content, and videos, all managed and logged automatically.

## Key Features

*   **Unified Telegram Interface:** Interact with your AI team via text or voice messages.
*   **Multi-Format Content Generation:**
    *   **Image Creation & Editing:** Generate new images and edit existing ones.
    *   **Written Content:** Create SEO-friendly blog posts and engaging LinkedIn posts.
    *   **Video Production:** Generate faceless videos on any topic.
*   **Image Database:** Search and manage a library of previously created images.
*   **Stateful Conversations:** Maintains context and memory of each chat for a natural user experience.
*   **Centralized Logging:** Automatically logs all created content to a Google Sheet.

## Workflow Architecture

The main workflow (`ldETapkr8Hg - 1.json`) acts as a central brain (Agent) that routes requests to specialized tools:

1.  **Trigger:** A Telegram message (text or voice) initiates the process.
2.  **Input Processing:** Voice messages are automatically transcribed to text.
3.  **AI Agent:** The core "Marketing Team Agent" (powered by GPT-4.1 via OpenRouter) analyzes the user's request and decides which tool to use.
4.  **Tool Execution:** The agent calls the appropriate sub-workflow to handle the task.
5.  **Response:** The final output (text, image link, confirmation) is sent back to the user via Telegram.

### Integrated Sub-Workflows (Tools)

The main workflow depends on these critical sub-workflows being imported into your n8n instance:
*   `Create Image` (ID: `lsZTPeThp35cB3Hs`)
*   `Edit Image` (ID: `nMBpMe21l4gDEjOI`)
*   `Search Images` (ID: `zDYAKGCIEChJa1JH`)
*   `Blog Post` (ID: `sS2JMp5z7YiqtJpa`)
*   `LinkedIn Post` (ID: `RgUBWsswXoQsX2tI`)
*   `Faceless Video` (ID: `7HwL0nnjhjdXJ3FY`)

## Prerequisites & Setup

### 1. Import Workflows
1.  **Import the Sub-Workflows:** First, import all six sub-workflows listed above into your n8n environment. The video tutorial by Nate Herk provides a link to download these templates from the free Skool community.
2.  **Import the Main Workflow:** Import the provided `AI Marketing Team.json` file (the decoded version of `ldETapkr8Hg - 1.json`).

### 2. Configure Credentials
You will need to set up the following credentials in n8n:
*   **Telegram:** For receiving messages and sending responses.
*   **OpenRouter:** To provide API access for the GPT-4.1 model.
*   **OpenAI:** For transcribing voice messages to text.
*   **Tavily** (inside Blog/Post workflows): For research capabilities.
*   **Google Sheets:** For logging content outputs.

### 3. Configure API Keys
Various sub-workflows require external API keys to function:
*   **Inside `Faceless Video` Workflow:**
    *   **PiAPI API Key:** For video generation.
    *   **Runway API Key:** For video processing.
    *   **ElevenLabs API Key:** For AI voice generation.
*   **Inside `LinkedIn Post` & `Blog Post` Workflows:**
    *   **Tavily API Key:** For web research.

### 4. Download and Connect Templates
*   **Creatomate Image Template:** Download from the Skool community and connect it in the relevant image generation nodes.
*   **Google Sheets Log Template:** Use [this template](https://docs.google.com/spreadsheets/d/1wQxM9cAwewCigPH22KDidMu_i9j_dx4MHEa5rmJiw5I/edit?usp=sharing) and connect its ID to the Google Sheets node in the sub-workflows for logging.

## Usage

1.  **Activate** the main workflow in n8n.
2.  Send a message to your Telegram bot. Examples:
    *   *"Create an image of a futuristic car on Mars"*
    *   *"Write a LinkedIn post about the benefits of no-code AI for small businesses, targeting entrepreneurs."*
    *   *"Edit the last image and add a rainbow in the sky."*
    *   *"Make a blog post about summer gardening tips for beginners."*
    *   *"Create a video about the history of the internet."*
3.  The AI agent will process your request, call the necessary tools, and send you the result directly in Telegram.

## Workflow Structure (n8n Nodes)

*   **Trigger:** `Telegram Trigger`
*   **Input Routing:** `Switch`, `Download Voice File`, `Transcribe Audio`, `Set`
*   **AI Core:** `Simple Memory` (Memory), `Think` (Reasoning), `GPT 4.1` (LLM), `Marketing Team Agent` (Orchestrator)
*   **Tools:** `Create Image`, `Edit Image`, `Search Images`, `Blog Post`, `LinkedIn Post`, `Video`
*   **Output:** `Telegram` (Response)


