# ShreeGattani-langsmith-MAT496
All thing which I learn in mat496 course (Introduction to large language model)--
**LANGSMITH**
# Module 0
I struggled to figure out how to set it up inside my conda environment. I learned how to use load_dotenv() to securely load environment variables (like API keys) instead of hardcoding them. I also cloned a GitHub repository and successfully ran a basic RAG application. Since it was a simple setup, my main modification was adding additional test questions to test my  AI’s performance.

# Module 1

### Video1
###  What I Learned
I learned how the **@traceable** decorator in LangSmith makes it very easy to log and visualize traces simply by adding it to a function. It automatically generates a **run tree** that captures every step in the application — including inputs, outputs, responses, and any errors. This detailed breakdown really helped me understand how data flows through the app and where performance can be improved. I also explored how to use **metadata**, where I attached details like app version or runtime info to each run. This made it much easier to **filter**, **analyze**, and **compare** runs in LangSmith. Together, the run tree and metadata gave me a complete, structured picture of my app’s execution and helped me spot optimization opportunities.
Notebook refrence - https://github.com/ShreeGattani/ShreeGattani-langsmith-MAT496/blob/main/Module%201/tracing_basics.ipynb

###  What I Did
Since the base code already covered most of the setup, I added a few extra test questions to observe how the **Trace Tree** and **metadata** behaved. Then, I extended the concept by creating a **Movie Recommender RAG system**. In this version, instead of static questions, I used a **vector retriever** that fetched movie-related data and passed it to the model to generate movie recommendations. Each function — from document retrieval to response generation — was traced using the **@traceable** decorator. I also passed metadata like query type and runtime details to analyze how each call appeared in the LangSmith desktop. This helped me understand how **LangSmith tracing** works end-to-end in a more realistic, multi-step RAG application.
Notebook refrence - https://github.com/ShreeGattani/ShreeGattani-langsmith-MAT496/blob/main/Module%201/tracing_basics_mywork.ipynb

### Video2
### What I have learned
Using tracing instead of traditional logging can greatly simplify debugging, especially in LLM applications where stack traces can be long and difficult to analyze. LangSmith addresses this challenge by offering a clean and organized interface that tracks each step of a run, making it much easier to pinpoint the source of errors. The platform allows specifying different run types through the @traceable decorator, such as LLM runs to interact with language models, Retriever runs to fetch data from external sources, Tool runs to execute specific functions, Chain runs to combine multiple operations, Prompt runs to prepare LLM inputs, and Parser runs to extract structured information. Moreover, LangSmith provides a Playground, a sandbox environment for quickly testing prompts and experimenting with workflows, which is available when using run_type="llm" or the default run_type="chain".
Notebook refrence- https://github.com/ShreeGattani/ShreeGattani-langsmith-MAT496/blob/main/Module%201/types_of_runs.ipynb

### what i did
I wrote code to test and demonstrate the use of LLM and Tool run types, both with and without tracing. I defined one function to summarize text directly and another function where the LLM decides how to summarize the text and whether to call the summarization tool.
Notebook refrence- https://github.com/ShreeGattani/ShreeGattani-langsmith-MAT496/blob/main/Module%201/types_of_runs_mywork.ipynb

