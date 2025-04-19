# AI-literacy Course module
Powerpoint Slides are provided.
![image](https://github.com/user-attachments/assets/93ab9c43-bb37-48ff-a345-acbba889b2ba)


# GraphRAG tutorial

GraphRAG is an advanced retrieval-augmented generation (RAG) system that reads text and organizes it into knowledge graphs for better AI information retrieval.

1. **Install Ollama.**  
   [https://ollama.com/](https://ollama.com/)

2. **Install Python 3.11 for compatibility.**  
   [https://www.python.org/downloads/release/python-3110/](https://www.python.org/downloads/release/python-3110/)

3. **Open Command Prompt (cmd terminal).**  
   - On Windows: Press Win + R, type in "cmd" and run.  
   - On Mac: Press Cmd + Space, then type "Terminal".

4. **Install Jupyter Lab.**  
   Run the following command in the terminal.
   ```bash
   pip install jupyterlab
   ```

5. **Install GraphRAG.**  
   Type the following in the terminal
   ```bash
   pip install graphrag==1.2.0

   ```

6. **Download Qwen2.5-7b-INT4 model (or a larger model if your hardware supports it).**  
   ```bash
   ollama pull qwen2.5:7b
   ```

7. **Create a GraphRAG folder and navigate to your GraphRAG folder in Jupyter Lab.**  
   For example, navigate using the file explorer on the left of Jupyter Lab, and open a new terminal or type these in a new terminal
   ```bash
   cd (Path to your GraphRAG folder)
   ```

8. **Create an 4k context length qwen2.5:7b LLM.**  
   Run this in the terminal. This step is necessary to avoid truncations of LLM output. This command generates a settings file in the terminal's current directory.
   ```bash
   ollama show qwen2.5:7b --modelfile > settings.txt
   ```

9. **Add this into the settings.txt:**
   ```
   PARAMETER num_ctx 4096
   ```

10. **Run this in the terminal to create the extended context model.**
    ```bash
    ollama create qwen2.5:7b_4k -f settings.txt
    ```

11. **Download the ClassDemo example from Canvas.**

12. **[Optional] In the ClassDemo example, open settings.yaml and inspect the settings to make sure:**  
    - The correct LLM model loaded.
    - The correct embedding loaded.
    - The request timeout is high (over 10000) if you’re not using a GPU.
    - Visualization settings meet GraphRAG guidelines.  
    [GraphRAG Visualization Guide](https://microsoft.github.io/graphrag/visualization_guide/)

13. **[Optional] Use autotune to do prompt tuning.**  
    The prompt is highly dependent on the input text because GraphRAG uses prompts to extract key entities from the text. (This step has been completed for you)  
    Run the following command for automatic prompt tuning:
    ```bash
    python -m graphrag prompt-tune --root ./ClassDemo --config ./ClassDemo/settings.yaml
    ```
    *Note: Autotune might occasionally fail with smaller LLMs (<72B). After tuning, review the updated prompt in the GraphRAG prompt folder and, if satisfactory, move it to the ClassDemo prompt folder.*

14. **Run this command to start the indexing process.**  
    This step may take longer than 1 hour if you do not have a GPU or a powerful CPU. Make sure you turn off auto sleep of your computer. You may complete this in the computer lab in Whitaker Hall. Those computers have an entry level GPU, but they will auto logout if you are away for more than 1 hour.
    ```bash
    graphrag index --root ./ClassDemo
    ```

15. **After it finishes, you can start to ask some questions:**
    
    - **Some general questions like summarization (use global query)**
      ```bash
      graphrag query --root ./ClassDemo --method global --query "Summarize this text into bullet points."
      ```

    - **Some specific questions (use local query)**
      ```bash
      graphrag query --root ./ClassDemo --method local --query "Which hospital did Fleming work at?"
      ```

16. **Use Gephi or other compatible software for knowledge graph visualization.**
