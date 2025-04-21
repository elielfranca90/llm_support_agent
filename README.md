# AI-Powered Customer Support Assistant for DeepDive 1000M Watch

This project implements an intelligent customer support system for the Abyss Precision DeepDive 1000M watch. The system combines a Flask backend with a Streamlit frontend to provide real-time, context-aware responses to customer inquiries about product specifications, warranties, maintenance, and technical support requests.

The assistant leverages LangChain and OpenAI's language models to process natural language queries and retrieve relevant information from product documentation. It maintains conversation history for personalized interactions and integrates with a SQLite database to track and respond to specific customer service requests.

## Repository Structure
```
.
├── app.py                 # Flask backend with LangChain integration and API endpoints
├── chat.py               # Streamlit frontend providing the chat interface
├── config.yaml           # Configuration file for API keys and model settings
├── cria_db.py           # Database initialization script for customer service requests
├── documents/           # Product documentation and reference materials
│   ├── Autorizadas.txt  # List of authorized service centers
│   ├── Garantia.txt     # Warranty terms and conditions
│   └── Manual.txt       # Product manual and specifications
└── requirements.txt     # Project dependencies
```

## Usage Instructions
### Prerequisites
- Python 3.8 or higher
- OpenAI API key
- SQLite3

### Installation

```bash
# Clone the repository
git clone <repository-url>
cd <repository-name>

# Create and activate virtual environment
python -m venv venv
source venv/bin/activate  # Linux/MacOS
venv\Scripts\activate     # Windows

# Install dependencies
pip install -r requirements.txt

# Initialize the database
python cria_db.py
```

### Quick Start
1. Configure your OpenAI API key in `config.yaml`:
```yaml
api_key:
  key: "your-api-key-here"
model:
  name: "gpt-4o-mini"
```

2. Start the Flask backend in a nohup session:
```bash
nohup python3 -m app.py &
```

3. In a new terminal, start the Streamlit frontend in a nohup session:
```bash
nohup python3 -m streamlit run chat.py
```

4. Access the chat interface at `http://localhost:8501`

### More Detailed Examples
1. Product Specifications Query:
```
User: "What is the water resistance of the DeepDive 1000M?"
Assistant: "The DeepDive 1000M has a water resistance of 1000 meters (100 ATM)."
```

2. Service Request Status:
```
User: "What is the status of atendimento 1?"
Assistant: [Returns status of service request #1 from database]
```

### Troubleshooting
Common Issues:
1. API Connection Errors
   - Error: "Unable to connect to OpenAI API"
   - Solution: Verify API key in config.yaml and internet connection
   - Debug: Check Flask logs at console output

2. Database Issues
   - Error: "No such table: atendimentos"
   - Solution: Run `python cria_db.py` to initialize the database
   - Location: Check for atendimentos.db in root directory

## Data Flow
The system processes customer inquiries through a multi-stage pipeline that combines document retrieval and conversational AI.

```ascii
User Input -> Streamlit Frontend -> Flask Backend -> [Document Retrieval (FAISS) | Database Query] -> LangChain Processing -> OpenAI API -> Response
```

Key Component Interactions:
1. Frontend sends user questions with unique client ID to backend
2. Backend checks for service request queries in SQLite database
3. If not a service request, queries vector store (FAISS) for relevant documentation
4. LangChain combines context, conversation history, and retrieved information
5. OpenAI model generates appropriate response
6. Response is stored in conversation history and displayed to user


Dicas para rodar
1. É necessário atualizar os pacotes
2. É necessário criar um venv, ativar e instalar os requirements.txt
3. É necessário atualizar o langchain: pip install --upgrade langchain