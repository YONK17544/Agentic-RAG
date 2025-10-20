Agentic RAG

Agentic RAG is an interactive AI-powered agent that simulates a restaurant waiter. The agent can answer customer questions about the menu, provide recommendations, and maintain friendly, professional interactions. This project demonstrates the use of LangChain, LangGraph, and OpenAI's GPT-based language models to create a robust agent workflow.

🧩 Features

Conversational AI agent acting as a restaurant waiter.

Handles both on-topic (menu-related) and off-topic questions gracefully.

Document retrieval: Uses a restaurant menu stored in Excel to answer customer queries.

Vector similarity search with FAISS for efficient retrieval of relevant menu items.

Dynamic conversation memory: Keeps track of the conversation history to provide context-aware responses.

Answer refinement: Improves the generated response to ensure politeness, clarity, and engagement.

Workflow management via StateGraph, allowing conditional branching and recursion for realistic conversation flow.

📦 Technologies & Libraries

LangChain & LangChain-Community: Language model integration and prompt templates.

LangGraph: Defines the agent workflow and state transitions.

OpenAI GPT Models (gpt-4o-mini): Natural language understanding and generation.

FAISS: Vector similarity search for retrieving relevant menu items.

Unstructured: Document loading and processing, specifically Excel menus.

Python: Core programming language for building the agent.

⚙️ Installation

Install the required libraries:

pip install -q langchain-community langchain-openai unstructured faiss-cpu langgraph

🔑 Setup

Store your OpenAI API key in Colab's user data with the key genai_course.

Place your restaurant menu Excel file (e.g., dim sum montijo.xlsx) in the project folder.

Load the API key in your notebook:

from google.colab import userdata
api_key = userdata.get('genai_course')

📝 Usage

Load the menu data:

from langchain_community.document_loaders import UnstructuredExcelLoader

loader = UnstructuredExcelLoader('dim sum montijo.xlsx', mode="elements")
data = loader.load()


Create embeddings and FAISS vector store:

from langchain_openai import OpenAIEmbeddings
from langchain.vectorstores.faiss import FAISS

embeddings = OpenAIEmbeddings(openai_api_key=api_key)
db = FAISS.from_documents(data, embeddings)


Define agent workflow with functions like greetings, check_question, retrieve_docs, generate, improve_answer, and further_question using StateGraph.

Run the agent:

from langgraph.graph import END

result = app.invoke({"start": True}, {"recursion_limit": 50})


The agent will greet the customer, answer questions about the menu, offer recommendations, and handle follow-up questions interactively.

🧠 Workflow

The agent workflow is managed with StateGraph:

Greetings: Start the conversation.

Check Question: Determine if the question is on-topic.

Retrieve Docs: Search the menu for relevant items.

Generate Answer: Create a response using GPT.

Improve Answer: Refine the response for friendliness and professionalism.

Further Question: Allow the customer to ask more questions.

Off-topic Handling: Provide polite responses for unrelated queries.

📷 Visualization

The workflow graph can be visualized using LangGraph:

display(Image(app.get_graph(xray=True).draw_mermaid_png()))

✅ Example Interaction

Customer: "What is your recommendation?"
Agent: "I recommend trying the Siao Long Pao, especially the Traditional version with pork, paksoy, and shiitake mushroom. Would you like more details or pairing suggestions?"

Customer: "Suggestions for pairing."
Agent: "The Traditional Siao Long Pao pairs beautifully with a glass of Lello White wine. The Shrimp Gyoza goes well with a refreshing Mint & Pineapple tea. Would you like to explore any specific drink options further?"

📂 Project Structure
Agentic-RAG/
│
├── dim sum montijo.xlsx       # Restaurant menu
├── agentic_rag_notebook.ipynb # Main Colab notebook
├── README.md                  # Project documentation
└── requirements.txt           # Python dependencies

💡 Highlights

Demonstrates Agentic RAG, LightRAG, and Agentic RAG concepts.

Combines retrieval-augmented generation (RAG) with structured workflows.

Focused on multi-turn conversations and context-aware answers.

Easily adaptable to other domains like customer support, FAQ bots, or retail assistants.

🔗 References

LangChain Documentation

LangGraph Documentation

OpenAI API

FAISS Library
