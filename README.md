# Real-time-weather-forecast
A weather app that integrates OpenAI's GPT model with OpenWeatherMap API to deliver precise and up-to-date weather forecasts.

## Overview

The Weather Information App provides real-time weather information for any location using OpenAI's GPT model and the OpenWeatherMap API. It leverages LangGraph workflow to process user input and retrieve accurate weather data.

## Features

- Extracts city name from user input.
- Retrieves weather information from OpenWeatherMap API.
- Provides temperature in both Celsius and Fahrenheit.

## Prerequisites

- Python 3.7 or higher
- pip for package management
- .env file for API keys

## Setup

1. **Clone the repository**

    ```bash
    git clone https://github.com/your-username/weather-info-app.git
    cd weather-info-app
    ```

2. **Create a virtual environment**

    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    ```

3. **Install the required packages**

    ```bash
    pip install -r requirements.txt
    ```

4. **Set up environment variables**

    Create a `.env` file in the root directory of the project and add your API keys:

    ```plaintext
    OPENWEATHERMAP_API_KEY=your_openweathermap_api_key
    OPENAI_API_KEY=your_openai_api_key
    ```

## Running the Application

1. **Run the Streamlit app**

    ```bash
    streamlit run app.py
    ```

2. **Open the app in your browser** at [http://localhost:8501](http://localhost:8501).

## Usage

1. Enter your location in the "Enter your location" field.
2. Click the "Get Weather" button to fetch weather information.
3. Review the weather report displayed on the screen.

## Code Overview

- **Environment Configuration**: Loads API keys from the `.env` file and sets up Langsmith tracing.
- **LangChain Workflow**: Defines a graph with nodes for extracting city names, fetching weather data, and providing temperature information.
- **Streamlit Interface**: Provides a user-friendly interface for inputting location and viewing results.

### Code Components

1. **Environment Setup**

    ```python
    load_dotenv()
    os.environ["OPENWEATHERMAP_API_KEY"] = os.environ.get("OPENWEATHERMAP_API_KEY")
    os.environ["OPENAI_API_KEY"] = os.getenv("OPENAI_API_KEY")
    ```

2. **Function Definitions**

    - `function_1`: Extracts city name from user input using GPT-3.5-turbo.
    - `function_2`: Fetches weather data using the OpenWeatherMap API.
    - `function_3`: Generates temperature information in Celsius and Fahrenheit.

3. **LangChain Graph Workflow**

    ```python
    workflow = Graph()
    workflow.add_node("agent", function_1)
    workflow.add_node("tool", function_2)
    workflow.add_node("responder", function_3)
    workflow.add_edge('agent', 'tool')
    workflow.add_edge('tool', 'responder')
    workflow.set_entry_point("agent")
    workflow.set_finish_point("responder")
    app = workflow.compile()
    ```

4. **Streamlit App Configuration**

    ```python
    st.set_page_config(page_title="Weather Information App", page_icon="🌦️", layout="wide")
    st.markdown("...")
    ```

## App Usage ScreenShorts

<img width="1397" alt="Screenshot 2024-07-29 at 5 12 57 PM" src="https://github.com/user-attachments/assets/cf904109-87e7-452b-a551-2e5779db3272">

## App Trace in LangSmith

<img width="1361" alt="Screenshot 2024-07-29 at 5 14 13 PM" src="https://github.com/user-attachments/assets/fc609376-073c-4ad7-8903-5656cc29de12">

## App workflow matplotlib graph

<img width="1038" alt="Screenshot 2024-07-29 at 5 23 01 PM" src="https://github.com/user-attachments/assets/f6dc0086-9400-4cb5-a477-9f493247c172">
