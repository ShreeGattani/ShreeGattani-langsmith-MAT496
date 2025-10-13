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

### Video 3: Alternative ways to trace
### What I have learned

The default method for setting up tracing is the @traceable decorator, which is typically sufficient when leveraging LangChain components within a graph. For more granular control, the with trace() context manager allows logging calls within a specific block of code. Additionally, metadata can be passed to both LangChain and LangGraph calls via the config argument in the invoke method. For users directly utilizing the OpenAI SDK, the wrap_openai() function traces all OpenAI calls. After wrapping the client, all subsequent calls are automatically traced to LangSmith. Metadata can also be included using the langsmith_extra field. Tracing is generally active by default once environment variables and LangChain/LangGraph are configured.

Link: https://github.com/ShreeGattani/ShreeGattani-langsmith-MAT496/blob/main/Module%201/alternative_tracing_methods.ipynb

### What i did:

I updated my existing chatbot to incorporate these alternative tracing methods: specifically with_trace() and wrap_openai(). I then documented the resulting changes and observations with screenshots from the LangSmith portal

Link: https://github.com/ShreeGattani/ShreeGattani-langsmith-MAT496/blob/main/Module%201/alternative_tracing_methods__mywork.ipynb

### Video 4: Conversational Threads
### What I have learned

Threads in LangSmith serve as an abstraction, grouping a series of traces that represent an application's invocation, essentially capturing a complete user interaction. They are created by including a uuid as a value pair within the metadata using the langchain_extra field. This feature is highly valuable for debugging a full human-LLM interaction that spans multiple traces.

Link: https://github.com/ShreeGattani/ShreeGattani-langsmith-MAT496/blob/main/Module%201/conversational_threads.ipynb

### What i did:

I redesigned my chatbot to track the entire conversation between the user and the LLM. I generated a new UUID for each conversation and passed it in the metadata. This allowed me to effectively group and track all related traces for a single conversational exchange. I included my observations and screenshots in the notebook.

Link: https://github.com/ShreeGattani/ShreeGattani-langsmith-MAT496/blob/main/Module%201/conversational_threads__mywork.ipynb

# MODULE 2

### Video 1: Dataset_upload

Datasets are lists of examples, comprising both inputs and outputs, used for rigorous testing and evaluating an LLM application, moving beyond simple "gut checks." I learned how to apply version tags to datasets, which is useful for testing an application's performance against older versions after making updates. Data can be added to a dataset directly from trace runs, manually, or by generating AI-powered examples. Schema ensures that all data, current and future, is stored in a consistent format. The concept of a split allows isolating critical examples for focused evaluation. Furthermore, datasets can be shared, downloaded, or cloned.

Link: https://github.com/ShreeGattani/ShreeGattani-langsmith-MAT496/blob/main/Module%202/dataset_upload.ipynb


### Video 2: Evaluators

Evaluators are functions or processes that score and quantify the performance of an LLM application or agent on specific test cases. They compare the expected output from a dataset example against the actual LLM output and assign a performance score. Evaluators can be defined using custom code directly in a Jupyter notebook or via the LangSmith website. It is also possible to use an LLM as a judge to perform the evaluation.

Link: https://github.com/ShreeGattani/ShreeGattani-langsmith-MAT496/blob/main/Module%202/evaluators.ipynb


### Video 3: Experiments

Experiments involve running an LLM application against a dataset and measuring its performance using defined evaluators. Experiments can be executed either through the SDK using the evaluate() function or via the LangSmith UI. I analyzed how changing the underlying LLM model impacted the evaluation results. I also learned to run experiments on specific subsets of examples, such as initial versions or specialized splits, and even on individual examples. The ability to run an experiment over a specific example multiple times (repetition) ensures consistent results. Experiments can also be configured with various parameters like repetition count, concurrent threads, and metadata.

Link: https://github.com/ShreeGattani/ShreeGattani-langsmith-MAT496/blob/main/Module%202/experiments.ipynb


### Video 4: Analysing experiments

I learned the process of systematically evaluating LLM applications using a combination of multiple evaluators—both code-defined (e.g., is_concise) and UI-configured (e.g., correctness). This allowed me to track performance trends over time as the application was iterated upon. The platform’s advanced filtering features enable isolation of specific model runs (like gpt-4o) and detailed side-by-side comparisons of experiments via summary charts and latency metrics. This provides empirical data to support deployment decisions. Most crucially, I gained the ability to deep dive into individual experiment runs and traces to see how each dataset example performed, allowing me to identify specific failure patterns and make confident, data-driven optimizations before pushing changes to production.

Link: https://github.com/ShreeGattani/ShreeGattani-langsmith-MAT496/blob/main/Module%202/analysing_experiments.ipynb

# MODULE 3

### Video 1: Playground
I have learned how can we use the playground feature in langsmith desktop and create prompt and modify it with the help of output sceema , repitations , adding a tool , asking question unrelated to prompt , adding sample questions to the prompt etc and i have shown everything in my notebook link i have provided below , as there were just twerking in the prompt so nothing much to change so i did that in my notebook itself.

### What i did:
Since this video contained breif introduction to playground and its features, I explored all of it with the tutorial and attached all of its screenshots in the notebook. along with that i had done both the things about changes and and what i learned in the same notebook.

Link: https://github.com/ShreeGattani/ShreeGattani-langsmith-MAT496/blob/main/Module%203/playground_experiments.ipynb

### Video 2: 
I've learned how to use prompt function in lagsmith desktop where i have learned how to create a prompt , call a prompt and upload a prompt and more that i have shown in my learning notebook and i have worked on normal notebook too and implemented everything as shown .

link: https://github.com/ShreeGattani/ShreeGattani-langsmith-MAT496/blob/main/Module%203/prompt_hub.ipynb

### What i did:
I did a little bit of twerking by my my own prompt of power ranger and modified it , played with it in langsmith and shown all the work with the help of the screenshots in following notebook

link: https://github.com/ShreeGattani/ShreeGattani-langsmith-MAT496/blob/main/Module%203/prompt_hub_mylearning.ipynb


