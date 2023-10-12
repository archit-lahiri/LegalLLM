# LegalLLM

UPDATE: The latest version of this chatbot (renamed to LegalLLM) has been uploaded to this repo in the [LegalLLM_Draft11 file](https://github.com/archit-lahiri/LegalLLM/blob/main/LegalLLM_Draft11). Here there is a drive link to two videos that demonstrate the working of the chatbot- part 1 and part 2. Part 1 is sufficient for understanding how it works.

I am very proud of how it has turned out and hope you definitely check it out :) 

I haven't uploaded the code yet but plan to in some time. It is different from the version 6 of the chatbot described below in it's internal analysis of law but still retains similar philosophy and working principles as verison 6. 


__________________________________________________________________________________________________________________________________________________________________________________________________

In this [notebook](https://github.com/archit-lahiri/Law-Helper-Chatbot/blob/main/lawbot-v6.ipynb) I implement a project idea I had to make a Law-Helper Chatbot. The goal of this project is to provide step by step situation relevant guidance to common citizens to approach the legal system. For this I use the langchain library to leverage openai llms to create a chatbot. For this I also feed documents like the **Indian Penal Code** and **Consumer Protection Act** and information from the internet is also retrieved.

Currently it is constrained to only work on cases of Consumer Law in India.

The project is currently divided into three phases:

**Initialization and set-up phase**:

->In this part the required libraries are downloaded and imported. The openai key is set.

->Functions that convert documents into vectorstores.



**Law Type Matching and Feedback Loop phase:**

->Function that leverages RAG (RetrievalQA chain) to match user query to a type of law. RAG is also used to determine which law in specific is broken from the law documents above.

->TOP-K uncertainty measuring method prompt as per the paper [Can LLMs Express Their Uncertainty? An Empirical Evaluation of Confidence Elicitation in LLMs](https://arxiv.org/abs/2306.13063) is used to match the user query to the top 3 laws in the relevant document and to also determine level of uncertainty for each law. 

->This uncertainty explains why the llm did not think the highest ranked law did not have an even higher confidence level. The way it is outputed means that the llm explains points of ambiguity in the situation. This ambiguity is used to ask the user questions or to ask another LLMChain (which has the knowledge of GPT-3.5-turbo) to give answers and reduce unceratinty in a feedback loop.

->Functions that use LLMChains to classify the unceratinty explanations into "search type" and "user query type" as well as LLMChains that convert the uncertainty explanations into simple questions for the user.

->Feedback loop function that combines all the above functions.



**Information Search and Parsing phase:**

->Customer agent (with search tool) using custom prompt template is inputed with all the context created from before and tasked with retrieving information using its search tool that creates information.

->Function that extracts information from the intermediate steps of the agent as that is where most of the relevant information is.

->Function that parses intermediate steps and outputs a step by step summary of what the user needs to know/can do. 


**THIS WORK IS STILL IN PROGRESS**





