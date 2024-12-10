## APAI4011 Project Group 8 Customer Service Demo File Instruction

We used the open source "[Langchain-Chatchat](https://github.com/chatchat-space/Langchain-Chatchat/blob/master/docs/contributing/README_dev.md)" Library for our Knowledge base and LLM management.

The code is based on Langchain-chatchat source code **under Linux environment**.

You also need to locally deploy another LLM service project called "[Xinference](https://inference.readthedocs.io/en/stable/getting_started/installation.html)" for running the LLM and Embedding model.

* To replicate our project, you should create a separate virtual environment, download, and run the LLM ``llama-3.1-instruct`` and embedding``bge-m3`` with xinference.

Create a vitual environment, make sure Python version is 3.11

```
conda create --name apai4011-customer-service python==3.11
conda activate apai4011-customer-service
```

Install dependencies of that chat using poetry:

```
pip install pipx
pipx install poetry
```

```
cd Langchain-Chatchat/libs/chatchat-server/
poetry install --with lint,test -E xinference
```

Before Run the code, you need to setup the data library in your environment.

```
export CHATCHAT_ROOT=/<path-to-the-root-folder>/apai4011-build/Langchain-Chatchat/libs/chatchat-server/langchain-data
```

Start the Langchain Service by:

```
cd ./Langchain-Chatchat/libs/chatchat-server
python chatchat/cli.py start -a
```

If you encounter error like this:

> 2024-11-29 21:28:17.413 | ERROR | chatchat.webui\_pages.utils:get:64 - TypeError: error when get /tools: Client.**init**() got an unexpected keyword argument 'proxies'

You can fix by ungrade python package "``httpx``" to version 0.27.2:

```
python -m pip uninstall httpx
python -m pip install httpx==0.27.2
```

Find the application at ``0.0.0.0:8501`` or your ip address with port number ``8501``.

Use ``RAG conversation`` with knowledge base ``Customer Service`` applied, and set ``knowledge matching threshold`` to around ``1.0-1.8`` for better results.

We setup the prompt of the LLM like this:

> You are an customer service specializt that specifically provide information for Chinese marchants who want to sell their products on Amazon. Never replied with "no answer based on exisiting information". Even if information contained in the knowledge base is no enough, you may mention everything you have relavant to the question as an answer.
> ![1733818239994](images/README/1733818239994.png)

Here is an example of a conversation we had:

![1733818197407](images/README/1733818197407.png)

Thanks for the talented developers of Langchain-Chatchat.

```
@software{langchain_chatchat,
    title        = {{langchain-chatchat}},
    author       = {Liu, Qian and Song, Jinke, and Huang, Zhiguo, and Zhang, Yuxuan, and glide-the, and liunux4odoo},
    year         = 2024,
    journal      = {GitHub repository},
    publisher    = {GitHub},
    howpublished = {\url{https://github.com/chatchat-space/Langchain-Chatchat}}
}
```
