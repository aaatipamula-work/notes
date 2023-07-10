<!--title: LLMs and AI -->
# Table of Contents <!-- omit in toc -->

`Important Sections are Italicized!`

- [Reference](#reference)
  - [*OpenAI Notes*](#openai-notes)
  - [*LangChain Notes*](#langchain-notes)
  - [LlamaIndex Notes](#llamaindex-notes)
    - [Query v.s. Chat Engines](#query-vs-chat-engines)
  - [*Database Connection Strings*](#database-connection-strings)
    - [Documentation Links](#documentation-links)
    - [Examples](#examples)
  - [Environment Setup](#environment-setup)
    - [Formatting](#formatting)
    - [Access](#access)
  - [Code Snippets](#code-snippets)
  - [Questions to Ask](#questions-to-ask)
  - [Thoughts](#thoughts)
    - [Ideas](#ideas)
    - [Problems](#problems)
    - [Watch](#watch)
    - [Solved](#solved)
- [Implementations](#implementations)
  - [*SQL Chain*](#sql-chain)
    - [Conceptual](#conceptual)
    - [Code Examples](#code-examples)
  - [*SQL Agent*](#sql-agent)
    - [Conceptual](#conceptual-1)
    - [Code Examples](#code-examples-1)
  - [LlamaIndex Implementation](#llamaindex-implementation)
    - [Conceptual](#conceptual-2)
    - [Code Examples](#code-examples-2)
  - [Schema Indexing](#schema-indexing)
    - [Conceptual](#conceptual-3)
    - [Process](#process)
    - [Changes to the Standard Implementation](#changes-to-the-standard-implementation)
    - [Improvements to be Made](#improvements-to-be-made)
  - [View Schema Prompt Injection](#view-schema-prompt-injection)
    - [Conceptual](#conceptual-4)
  - [Prompt Injection](#prompt-injection)

# Reference

## *OpenAI Notes*

[General Docs](https://platform.openai.com/docs/introduction)

Most of the following is links to reading and resources that could be helpful when looking into OpenAI and GPT:

- [OpenAI Cookbook](https://github.com/openai/openai-cookbook)
    - A Github repo of useful links and resources.
- [OpenAI Models](https://platform.openai.com/docs/models) 
    - A list of all the models OpenAI currently has for use.
- [Best Practices for GPT](https://platform.openai.com/docs/guides/gpt-best-practices)
    - Guidelines from OpenAI on how to instruct models.
- [Best Practices for Safety](https://platform.openai.com/docs/guides/safety-best-practices)
- [Best Practices for Production](https://platform.openai.com/docs/guides/production-best-practices)


## *LangChain Notes*

[Python Docs](https://python.langchain.com/docs/get_started)

[Github](https://github.com/hwchase17/langchain)

A fairly popular python/js framework to use for LLM AI prompting and management.

The following are some of the python docs LangChain has on useful topics to get familiar with some how the framework and how LLM generative AI works in general:

- [Environment Setup](https://python.langchain.com/docs/get_started/quickstart#environment-setup)
  - Setting up your python program.
  - Also refer to my [notes](#environment-setup)
- [Prompts](https://python.langchain.com/docs/modules/model_io/prompts/)
  - Good to understand how this works first.
- [LLM v.s. Chat Models](https://python.langchain.com/docs/modules/model_io/models/)
- [Overview of Data Connection](https://python.langchain.com/docs/modules/data_connection/)
  - Connecting SQL databases, processing documents etc.
- [What are Chains?](https://python.langchain.com/docs/modules/chains/)
- [What are Agents?](https://python.langchain.com/docs/modules/agents/)
- [Adding Memory](https://python.langchain.com/docs/modules/memory/)
  - For both Agents and Chains.
- [Callbacks](https://python.langchain.com/docs/modules/callbacks/)
  - Hooking into the function calls being made, useful for logging and looking at an agent or chains's "thought process" 

Most of these are not very long, just conceptual overviews with a few examples written in python. I found them to be a good starting point to understand how something works and then diving deeper from there.


## LlamaIndex Notes

[Python Docs](https://gpt-index.readthedocs.io/en/latest/index.html)

[Github](https://github.com/jerryjliu/llama_index)

This is a framework that improves upon LangChain and makes it easier to link data.

From what I've tried its fairly slow, and doesn't seem to offer much in the way of use flexibility. I may come back to this but for now I'm focusing on LangChain.

Pros:
- It may provide more accurate queries.

Cons: 
- Less control over implementation. 

### Query v.s. Chat Engines

- Query engines are solely focused on answering the question, they do not retain context and are similar in nature to an SQL Chain
- Chat engines are more conversational, but slightly more prone to injecting irrelevant context into answers.


## *Database Connection Strings*

### Documentation Links

- [MSSQL Connections](https://docs.sqlalchemy.org/en/20/dialects/mssql.html#module-sqlalchemy.dialects.mssql.pyodbc)
    - Additional Info
- [Engine Connections](https://docs.sqlalchemy.org/en/20/tutorial/engine.html)
    - Use if using a different connection other than MSSQL

### Examples

[LangChain](#langchain-notes) uses [SQLAlchemy](https://www.sqlalchemy.org/) (A Python Object Relational Mapping library) for SQL database connection

The following code works if you are implicitly authenticating with the user you are logged in as on a Windows machine for MSSQL Server using LangChain's SQLDatabase wrapper: 

```python
from langchain import SQLDatabase

server = "hostname_or_ip"
database = "databasename"

db = SQLDatabase.from_uri(
    "mssql+pyodbc://"+server+"/"+database+"?driver=ODBC+Driver+17+for+SQL+Server"
)
```

If you are authenticating with SQL credentials instead use the following:

```python
from langchain import SQLDatabase

server = "hostname_or_ip"
database = "databasename"
username = "usernamehere"
password = "passwordhere"

db = SQLDatabase.from_uri(
    f"mssql+pyodbc://{username}:{password}@{server}/{database}?driver=ODBC+Driver+17+for+SQL+Server"
)
```


## Environment Setup

### Formatting

Environment Variables are formatted in all capitalized letters and with underscores such as the following: 

```sh
API_TOKEN_XYZ="key_here"
```

### Access

This is relatively simple in Python, refer to the following: 

```python
import os

ENV_VARIABLE = os.environ.get("API_TOKEN_XYZ")
```

There are 3 ways I would suggest you set [Environment Variables](https://en.wikipedia.org/wiki/Environment_variable) 
    - dotenv
    - Command line
    - Hard code

It is standard to keep the formatting of constant variables and loaded environment variables in the same [formatting](#formatting) as environment variables.

**dotenv**

I would suggest this method as its usually pretty versatile and a standard in Python

Simply download the dotenv library with:

```shell
pip install python-dotenv --upgrade
```

and use it in your code by putting the following at the top of the file you're running:

```python
from dotenv import load_dotenv

load_dotenv("/path/to/.env")
```

It is customary to name your Environment Variables file `.env`. Refer to [formatting](#formatting) for how to structure the file and [access](#access) on how to grab the values of the env variables.

**Command line**

Before running your program run the following command in your command line:

```shell
export API_TOKEN_XYZ="token_here"
``` 

*NOTE*: Make sure not to put any spaces on either side of the `=` character, this will lead to errors.

Refer to [access](#access) on how to grab the values of the env variables.

**Hard Code**

I would not suggest you use this method, but if you would like to use the following code: 

```python
import os

os.environ["API_TOKEN_XYZ"] = "token_here"
```

Refer to [access](#access) on how to grab the values of the env variables.


## Code Snippets

This is a useful function to interact with an Agent or Chain in the command line:

```python
from langchain import SQLDatabaseChain
from langchain.agents import AgentExecutor

def mainEventLoop(aiObject: AgentExecutor | SQLDatabaseChain):
    while True:
        try: 
            userInput = input("User: ")
            if userInput.lower() in ["exit", "close"]:
                print("Exiting...")
                exit(0)
            ai_response = aiObject.run(userInput)
            print(f"AI: {ai_response}")

        except KeyboardInterrupt:
            print("Exiting...")
            exit(0)
        
        except InvalidRequestError as err:
            print(f"{err._message}")
```


## Questions to Ask

- How many tickets were created in the month of may?
- Group those tickets by status.


## Thoughts

### Ideas 
- If an API exists and uses the OpenAPI standard, we can create a program to parse and create queries for the API similar to the examples above.
- Try using Views
  - **Implementation**: Remove any tools to query the schema and tables, just inject into the prompt. Guide through prompting.
- *Get rid of the ID Columns, we only use those to refrence specific things and it would muddy the prompt fed to the LLM*
- *Hard Code in a WHERE col = 'val' to prevent peeking into other users data*

### Problems
- Too many tokens throws an error
  - **Idea**: `try except` block. 
  - **Idea**: Token limits
- *Missing some input keys: {'input'}*
  - Not sure how to solve this one tbh 
- Understanding
  - ![context](./pictures/understanding.png)
  - **Idea**: Change the [model](#openai-notes)
  - Not sure how to solve this yet
- Repetitition
  - ![context](./pictures/repetition.png)
  - **Idea**: Change the [model](#openai-notes)

### Watch
- Doesn't pick up correct Status:
  ![context](./pictures/wrongstatus.png)
  - **Idea**: Create a tool
    - This is working somewhat, the only problem is that the llm is putting more than one word as an input.
    - Create a tool to list all the statuses.
  - *Potential Solution*: Prompting
    - ![context](./pictures/sdcasestatus.png)
    - This works for specific things but I would have to add a line for every status which would compound really fast.
    - Found a better way that just lists all the possible values.
     > Values in the sdCaseStatusDesc column can only be the following: Approved, Waiting For Triage, Parking Lot, On Hold, In Requirements, In Development Queue, Researching, Being Worked, Waiting for Customer, Pending Additional Information, Ready for QA, In UAT, Waiting to be Released, Resolved, To Be Scheduled, Pending Approval, In QA
  - *Potential Solution*: Added the following code to list out possible values in columns
    ```python
    from typing import List
    from langchain import SQLDatabase

    class SQLDatabaseExt(SQLDatabase):

    def col_values(self, columns: List[str], table: str):
        fin_str = ""
        for col in columns:
            query = f"SELECT {col} from {table} GROUP BY {col}"
            fin_str += f"Values in the {col} column can only be one of the following\n{self.run_no_throw(query)}\n\n"
    ```
- Not using count where applicable
  - *Potential Solution*: Add the following to the prompt:
    > Use aggregate functions such as COUNT and GROUP BY when asked about quantities.
- Uses name from context when not applicable
  ![context](./pictures/context.png)
  - **Idea**: Prompt this out.
  - *Potential Solution*: Add the following line to the prompt
    > Disregard previous conversation history when not related to the question.
- User Names:
  - *Potential Solution*: Create a tool to grab user names and ids when question prompts for a user
    ```python
    class QueryUserNames(BaseTool):
        """Tool for getting the correct user name."""

        db: SQLDatabase

        name = "grab_user_name"
        description = """
        Input to this tool is the name of a user provided by a question. This will output the UserId and the full UserName of the inputted user if there is no relevant user found nothing will be given back. 
        """

        def _run(
            self,
            query: str,
            run_manager: Optional[CallbackManagerForToolRun] = None,
        ) -> str:
            """Execute the query, return the results or an error message."""
            return self.db.run_no_throw(f"SELECT TOP 1 * FROM AI_UserIDXNameView WHERE Username LIKE '%{query}%'")

        async def _arun(
            self,
            query: str,
            run_manager: Optional[AsyncCallbackManagerForToolRun] = None,
        ) -> str:
            raise NotImplementedError("QuerySqlDbTool does not support async")
    ```
  - **Idea**: Use First and Last Name columns, prompt to search using both columns
  - **Idea** ***Deprecated***: Indexing User Names and Injecting them into the prompt

### Solved
- Question Semantics:
  - *Solved*: Should be solved by [Views](#ideas) but bugs may pop up.
- Understanding Table Joins (Relationships between Tables)
  - *Solved*: Using [Views](#ideas) to flatten out tables.
- Doesn't specify a year 
  - *Solved*: Inserted a line in the prompt to specify year
  > Always use the year {year} unless a year is specified in a question.
- Memory
  - *Solved*: Added `ConversationWindowBufferMemory` to the Agent Executor


# Implementations

Things I've tried to connect an SQL database with AI

## *SQL Chain*

[Python Docs](https://python.langchain.com/docs/modules/chains/popular/sqlite)

### Conceptual 


- Similar to how ChatGPT works, you give the LLM a directive and when it gets a question it crafts a query to use, extracts information and answers the question.

Pros: 
- Using an sql chain could be beneficial as you can choose if data is exposed to the api.
- Easier to tweak behavior. 

Cons: 
- However sql chains not very effective when crafting complex queries. 
- Can only really answer simple questions about very simple schemas

### Code Examples

This is an example of a chain that uses a custom prompt:

```python
from dotenv import load_dotenv
from langchain import OpenAI, SQLDatabase, SQLDatabaseChain, PromptTemplate

load_dotenv("/path/to/.env")

server = "hostname_or_ip"
database = "databasename"

llm = OpenAI(temperature=0, verbose=True)
db = SQLDatabase.from_uri(
    "mssql+pyodbc://"+server+"/"+database+"?driver=ODBC+Driver+17+for+SQL+Server",
)

dbtemplate = """
Given an input question, first create a syntactically correct {dialect} query to run, then look at the results of the query and return the answer.
Use the following format:

Question: "Question here"
SQLQuery: "SQL Query to run"
SQLResult: "Result of the SQLQuery"
Answer: "Final answer here"

Only use the following tables:
characters
organization

Question: {input} """

dbprompt = PromptTemplate(
    input_variables=["input", "dialect"],
    template=dbtemplate
)

db_chain = SQLDatabaseChain.from_llm(
    llm=llm,
    db=db, 
    prompt=dbprompt, 
    verbose=True, 
    # Check if the query that the Chain comes up with is valid
    use_query_checker=True, 
)
```

It can be run with the following:

```python
db_chain.run(input("Question: "))
```

Refer to [code snippets](#code-snippets) for a simple command line interface.


## *SQL Agent*

[Python Docs](https://python.langchain.com/docs/modules/agents/toolkits/sql_database)

### Conceptual

- Based on the sql chain, it uses multiple queries to the API to break the larger question into smaller ones it will answer to produce a final answer.

Pros:
- This will usually execute the sql queries fairly well returning a concise answer.
- Much better with complex schemas and sometimes picks up on context in vague questions.

Cons: 
- Not very conversational and only give direct answers.
- Its slightly experimental as of right now
- Less control over how the bot behaves.

Other Considerations:
- Could fine tune prompt and instruction set for the sql agent by making a custom agent.

### Code Examples

This is much simpler as most of the setup is relegated to the langchain framework but it is highly customizable if wanted.

```python
from dotenv import load_dotenv
from langchain import OpenAI, SQLDatabase
from langchain.agents import create_sql_agent
from langchain.agents.agent_toolkits import SQLDatabaseToolkit

load_dotenv("/path/to/.env")

server = "hostname_or_ip"
database = "databasename"

llm = OpenAI(temperature=0, verbose=True)
db = SQLDatabase.from_uri(
    "mssql+pyodbc://"+server+"/"+database+"?driver=ODBC+Driver+17+for+SQL+Server",
)
toolkit = SQLDatabaseToolkit(db=db, llm=llm)

agent_executor = create_sql_agent(
    llm=llm,
    toolkit=toolkit,
    verbose=True
)
```

It can be run with the following: 

```python
agent_executor.run(input("Question: "))
```

Refer to [code snippets](#code-snippets) for a simple command line interface.


## LlamaIndex Implementation

### Conceptual

- Index the schema of the database and use that to procure the correct tables

### Code Examples

The following is a custom class I made that generates the SQL Database's index and creates a query or chat engine.

```python
# Typing imports
from typing import Union, Optional, List, Any
from llama_index.response.schema import RESPONSE_TYPE
from llama_index.indices.query.schema import QueryType
from llama_index.indices.query.base import BaseQueryEngine
from llama_index.chat_engine.types import BaseChatEngine


import os
from llama_index import SQLStructStoreIndex, SQLDatabase, VectorStoreIndex, StorageContext, load_index_from_storage
from llama_index.indices.struct_store import SQLContextContainerBuilder
from sqlalchemy import create_engine, URL

# Wrapper around the process of creating and SQL Query Engine
class SQLAIEngineGenerator:
    def __init__(
            self, 
            url: Union[str, URL], 
            query_string: QueryType, 
            tables: Optional[Union[List[str], None]] = None,
            debug: bool = False,
            **kwargs
        ) -> None:
        """
        A wrapper around the setup of a query or chat engine. The class simply creates an index for a query and chat engine to be initiated. Class methods are then used to generate the Chat engine and the Query engine.

        Args:
        url: URL connection string for the SQLAlchemey engine. Refer to SQLAlchemy docs for more information.
        tables: Tables to include within the database.
        query_string: An example question to ask the engine to identify the context.
        debug: add logging for debugging
        """

        if debug:
            # Lazy load
            import logging

            logging.basicConfig(filename="index.log", filemode="w", level=logging.DEBUG)

        # Error if no OpenAI key detected
        if os.environ.get("OPENAI_API_KEY")  is None:
            raise KeyError("No OpenAi API key found.")

        # Define database and create and store schema
        engine = create_engine(url)
        database = SQLDatabase(engine, include_tables=tables)
        context_builder = SQLContextContainerBuilder(database)

        db_schema_index = context_builder.derive_index_from_context(
            VectorStoreIndex, 
            store_index=True,
            **kwargs
        )

        context_builder.query_index_for_context(
            db_schema_index,
            query_string,
            store_context_str=True
        )

        context_container = context_builder.build_context_container()

        self.index = SQLStructStoreIndex(
            [],
            sql_database=database,
            sql_context_container=context_container,
            **kwargs
        )

    def create_chat_engine(self) -> BaseChatEngine:
        return self.index.as_chat_engine()
    
    def create_query_engine(self) -> BaseQueryEngine:
       return self.index.as_query_engine()
```


## Schema Indexing

A somewhat of what [LlamaIndex](#llamaindex-implementation) does but with some improvements to flexibility

### Conceptual 

- Creates an index of the databases schema to use for reference.
- At query time it identifies the relevant tables and injects it into the prompt

### Process

- Generate an Index of the Database Schema
    - This can be done from a file (and updated if needed)
    - This can also be directly done from the database
- Append context
    - This can be automatically generated by the llm or manually written out by a user
- Generate documents 
    - Each document contains a table, its schema, and context for the table
- Feed documents to a vector store database
- Initiate an agent with a retrieval tool that queries the vector store database for the correct tables

### Changes to the Standard Implementation

- Uses an index of the Schema *with context* to produce the correct tables.
- Hard Coded the use of DROP, UPDATE, DELETE, INSERT, LIMIT as unusable.
- Custom Prompting to encourage correct actions and "thoughts"

### Improvements to be Made

- Use a more robust vector store DB
- Changes to Prompting
- Concurrency (asynchronus function calls)

## View Schema Prompt Injection

### Conceptual

- Simply create a view with all the applicable data and inject the schema of the view into the prompt

## Prompt Injection

***Have not tried this yet***

A system where a user sends a prompt to our program and we modify that prompt with data stored from a database and then send it to the OpenAI API. 

[Promptify](https://github.com/promptslab/Promptify) is a NLP (Natural Language Processing) library that may be useful for this idea.

Pros:
- Minimal use of the gpt api
- We get to choose what information to send to the api

Cons: 
- Would have to create a system to figure out what information to include and send to the API. 
- May have to create an entirely different system to find the relevant information to include.


[def]: #environment-setup