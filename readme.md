# Essay Writing Assistant

**An AI-powered tool for generating, refining, and managing 3-paragraph essays using LangGraph, GPT-3.5-turbo, Tavily, and Gradio.**

This project is an interactive essay-writing assistant that leverages AI to plan, research, draft, and critique short essays. Built with LangGraph for state management, OpenAI's GPT-3.5-turbo for text generation, Tavily for web research, and Gradio for a user-friendly GUI, it provides a modular and extensible framework for essay creation.

## Features
- **Essay Planning**: Generates a high-level outline for a 3-paragraph essay based on a user-provided topic.
- **Research Integration**: Uses Tavily to fetch relevant content from the web to enrich essays.
- **Draft Generation**: Produces a draft essay based on the plan and research, with iterative revisions.
- **Critique & Refinement**: Provides detailed feedback on drafts and supports multiple revision cycles.
- **Interactive GUI**: A Gradio-based interface to manage the essay-writing process, including live output, state management, and thread switching.
- **State Persistence**: Uses SQLite for checkpointing to maintain the agent's state across interactions.

## Prerequisites
- Python 3.8 or higher
- API keys for:
  - OpenAI (for GPT-3.5-turbo)
  - Tavily (for web search)
- Required packages (see `requirements.txt`)

## Installation

1. **Clone the Repository**
   ```bash
   git clone https://github.com/<your-username>/essay-writing-assistant.git
   cd essay-writing-assistant
   ```

2. **Set Up a Virtual Environment** (recommended)
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure Environment Variables**
   - Create a `.env` file in the project root:
     ```plaintext
     OPENAI_API_KEY=your-openai-api-key
     TAVILY_API_KEY=your-tavily-api-key
     ```
   - Obtain API keys:
     - OpenAI: [Sign up here](https://platform.openai.com/signup)
     - Tavily: [Register here](https://tavily.com/)

## Usage

1. **Run the Application**
   ```bash
   python main.py
   ```
   - If no `PORT1` environment variable is set, the app runs locally. Otherwise, it uses the specified port (e.g., for deployment).

2. **Interact via the Gradio Interface**
   - Open your browser to the provided URL (e.g., `http://localhost:7860`).
   - Enter an essay topic (e.g., "Pizza Shop") in the "Agent" tab.
   - Click "Generate Essay" to start the process or "Continue Essay" to resume.
   - Use tabs ("Plan", "Research Content", "Draft", "Critique") to view and modify outputs.
   - Manage threads and states via dropdowns in the "Manage Agent" accordion.

3. **Customization**
   - Adjust `max_revisions` in `writer_gui.run_agent` (default: 2) for more/fewer revision cycles.
   - Modify prompts in `ewriter.__init__` to change the AI’s behavior.

## Project Structure
```
essay-writing-assistant/
├── main.py              # Entry point to launch the app
├── ewriter.py           # Core essay-writing logic (if separated)
├── requirements.txt     # Dependencies
├── .env                 # Environment variables (not tracked)
└── README.md            # This file
```

## Example
- **Input Topic**: "The Impact of Social Media"
- **Output**:
  - **Plan**: Outline with 3 headers (e.g., Introduction, Benefits, Drawbacks).
  - **Research**: Web content snippets from Tavily.
  - **Draft**: A 3-paragraph essay.
  - **Critique**: Feedback on depth, style, etc.

## Troubleshooting
- **API Errors**: Verify API keys in `.env` and ensure you have an active internet connection.
- **Gradio Issues**: Check port availability or set `share=True` for public access.
- **State Errors**: Clear the SQLite memory by restarting the app if unexpected behavior occurs.

## Contributing
1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/new-feature`).
3. Commit changes (`git commit -m "Add new feature"`).
4. Push to the branch (`git push origin feature/new-feature`).
5. Open a pull request.

## License
This project is licensed under the MIT License. See [LICENSE](LICENSE) for details (if applicable).

## Acknowledgments
- Built with [LangGraph](https://github.com/langchain-ai/langgraph), [OpenAI](https://openai.com/), [Tavily](https://tavily.com/), and [Gradio](https://gradio.app/).
- Created as of March 19, 2025.
```

---

### requirements.txt

```plaintext
# Core dependencies for the essay-writing assistant
langgraph==0.1.0  # For state graph management (version approximate, adjust as needed)
langchain-openai==0.1.0  # For OpenAI integration
langchain-core==0.1.0  # Core LangChain utilities
tavily-python==0.2.0  # Tavily API client (version approximate)
gradio==4.20.0  # For the GUI
openai==1.10.0  # OpenAI SDK
pydantic==1.10.0  # For structured outputs
sqlite3  # Built-in Python, no pip install needed
python-dotenv==1.0.0  # For loading .env files
```

#### Notes on Versions:
- Versions are approximate and based on typical releases as of early 2025. You may need to adjust them based on compatibility:
  - Check the latest versions with `pip install package_name --upgrade`.
  - `langgraph` and related packages might not have stable releases yet; use the latest from GitHub if needed (e.g., `pip install git+https://github.com/langchain-ai/langgraph.git`).
- `sqlite3` is included in Python’s standard library, so no separate installation is required.

---

### Additional Steps
1. **Create `main.py`** (if not already present):
   ```python
   from ewriter import ewriter
   from writer_gui import writer_gui

   if __name__ == "__main__":
       agent = ewriter()
       gui = writer_gui(agent.graph, share=False)
       gui.launch()
   ```
   - Save this as `main.py` in your project root to match the README’s usage instructions.

2. **Test the Setup**:
   - Ensure you have valid API keys in `.env`.
   - Run `pip install -r requirements.txt` and `python main.py` to verify everything works.
