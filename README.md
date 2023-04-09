# GPT-4 & LangChain - ChatBot for PDF Documents

In this project, the new GPT-4 API is utilized to create chatbot based on multiple large PDF files.

Tech stack for the project involves LangChain, Pinecone, Typescript, OpenAI, and Next.js. LangChain is a framework that makes it easier to build scalable AI/LLM apps and chatbots. Pinecone is a vectorstore for storing embeddings and your PDF in text to later retrieve similar docs.

[Tutorial video](https://www.youtube.com/watch?v=ih9PBGVVOO4)

A well-designed visual diagram showing the architecture used in this project can be found in the `visual guide` folder.
Kudos and thanks to [@mayowaoshin](https://twitter.com/mayowaoshin)

**If you run into errors, please review the troubleshooting section further down the page.**

## Development - How to Use

1. Clone the repo

```
git clone [github https url]
```

2. Install packages

```
pnpm install
```

3. Set up your `.env` file

- Create your own `.env` file and then copy the content of `.env.example` into your newly created `.env` file
  Your `.env` file should look like this:

```
OPENAI_API_KEY=

PINECONE_API_KEY=
PINECONE_ENVIRONMENT=

PINECONE_INDEX_NAME=

```

- Visit [openai](https://help.openai.com/en/articles/4936850-where-do-i-find-my-secret-api-key) to retrieve your API key and insert it into your `.env` file.
- Visit [pinecone](https://pinecone.io/) to create and retrieve your API key. Also, don't forget to retrieve your environment and index name from the dashboard.

4. In the `config` folder check the `pinecon.ts` file to replace the `PINECONE_NAME_SPACE` with a `namespace` where you'd like to store your embeddings on Pinecone when you run `pnpm run ingest` command. This namespace will later be used for queries and retrieval.

5. In `utils/makechain.ts` change the `QA_PROMPT` variable for your own usecase. This prompt determines how the AI agent would respond to your questions. Also, change `modelName` in `new OpenAIChat` block to `gpt-3.5-turbo`, if you don't have access to `gpt-4`. Before using hte GPT-4 as your model, please verify outside this repo that you are granted access to `gpt-4`, otherwise the application will not work with it.

## Embeddings - How to Embed Your PDF Files

**This repo can load multiple PDF files**

1. Inside the `docs` folder, add your pdf files or folders that contain your pdf files.

2. Run the script `npm run ingest` to 'ingest' and embed your docs. If you run into errors troubleshoot below.

3. Check Pinecone dashboard to verify your namespace and vectors have been added.

## Running in Local Dev Environment - How to Start the App

Once you've verified that the embeddings and content have been successfully added to your Pinecone, you can run the app `pnpm run dev` to launch the local dev environment, and then type a question in the chat interface.

## Troubleshooting

In general, keep an eye out in the `issues` and `discussions` section of this repo for solutions.

**General errors**

- Make sure you're running the latest Node version. Run `node -v`
- Try a different PDF or convert your PDF to text first. It's possible your PDF is corrupted, scanned, or requires OCR to convert to text.
- `Console.log` the `env` variables and make sure they are exposed.
- Make sure you're using the same versions of LangChain and Pinecone as this repo.
- Check that you've created an `.env` file that contains your valid (and working) API keys, environment and index name.
- If you change `modelName` in `OpenAIChat` note that the correct name of the alternative model is `gpt-3.5-turbo`
- Make sure you have access to `gpt-4` if you decide to use. Test your openAI keys outside the repo and make sure it works and that you have enough API credits.
- Check that you don't have multiple OPENAPI keys in your global environment. If you do, the local `env` file from the project will be overwritten by systems `env` variable.
- Try to hard code your API keys into the `process.env` variables.


**Pinecone errors**

- Make sure your pinecone dashboard `environment` and `index` matches the one in the `pinecone.ts` and `.env` files.
- Check that you've set the vector dimensions to `1536`.
- Make sure your pinecone namespace is in lowercase.
- Pinecone indexes of users on the Starter(free) plan are deleted after 7 days of inactivity. To prevent this, send an API request to Pinecone to reset the counter before 7 days.
- Retry from scratch with a new Pinecone project, index, and cloned repo.

## Credit

This repo is adapted from [mayooear/gpt4-pdf-chatbot-langchain](https://github.com/mayooear/gpt4-pdf-chatbot-langchain)
Frontend of this repo is inspired by [langchain-chat-nextjs](https://github.com/zahidkhawaja/langchain-chat-nextjs)
