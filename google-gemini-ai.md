#


## What is Gemini
Gemini is a series of multimodal generative AI models developed by Google. Gemini models can accept text and image in prompts, depending on what model variation you choose, and output text responses. You can intercate via API or the App

We'll do:
* Text to Text: When the prompt input includes only text, use the gemini-pro model with the `generateContent` method to generate text output

* Text/Image to text:When the prompt input includes both text and images, ise the gemini-pro-vision model with the `generateContent` method to generate text output.

* Text to Chat: to build a multi-turn conversation, use the gemini-rpo model, and utilize the chat by calling `startChat()`. Then use `sendMessage()`

* Text to Embedding: Use **embedding-001** model with the `embedContent` method to generate embeddings.

## What's AI
Artificial Intelligence is the simulation of human intelligence processes by machines, we say simulation because AI is not sentient, meaning it cannot think for itself, often when we say AI we most of the time are referring to **Machine Leaning**.

**Machine Learning**: Machine learning works by using large amounts of training data, that is then analyzed for correlations and patterns

**Large Language Models** (LLMs) are machine learning models that can comprehend and generate human language text. Sometimes they're referred to as AI models that can comprehend and generate human language text.

At their most basci level, LLM are like sophisticated autocomplete applications. We can train models to take an input of Text such as "You can lead a horse to water..." and have the LLM text ouput text statistically return "..but you can't make it drink it." as the text suggestingis based on patterns learned from the training data. You can use this to:
- Generate poetry, short stories, blog posts
- Convert structure of data to freeform text
- Summarize information
- Generate code
- Translate
- Build a chatbot

When you prompt an LLM its text response is generated in two stages. In the first stage the LLM process the input prompt and generates a probability distribution over possible Tokens or Words thata  likely to come next. For example if you prompt with the  input text "The dog jumped over the fence.." the LLM will produce an array of probably next words `[("fence", 0.77), ("ledge", 0.12), ("blanket", 0.03)..]. This process is deterministic, the LLM will produce the same distribution every time you write the same "input".

In the second stage, the LLM converts this distributions into actual text responses through one of several decoding strategies. A simple decoding strategy might select the most likely token at every time step this process wull always be deterministi however you could choose to randomly sampling over the distribution returned by the model. You can select the level of Randomness allowed by setting the **temperature**. A temperature of 0 means only the most likely tokesn are selected, leaving the most ranmdon and expected to higher temperatures

https://ai.google.dev/gemini-api/docs/api-key

## Tokenisation
When using long prompts it might be usefeul to count tokens before sending any content to the model. If you want to be specific you can use one of the models at our disposal

**Tokens**: Token are what all the models use to process text. They are essentially common sequences of characters found in text.

As a rule of thumb for a gemini model a toke is equivalent to about 4 characters, so a 100 Tokens are about 60 to 80 words

## Project

Requirements:
- Node.js ^18
- npm
- SDK `npm install @google/generative-ai`

1) Get your API key in https://aistudio.google.com/app/apikey
2) Test your API key, using the curl command given after you get your API key
```
curl \
  -H 'Content-Type: application/json' \
  -d '{"contents":[{"parts":[{"text":"Whats the most popular song from the InkSpots"}]}]}' \
  -X POST 'https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent?key=XXXXyour Key Here XXXXXXXX'
```
To which you will get the following Reply:
```json
{
  "candidates": [
    {
      "content": {
        "parts": [
          {
            "text": "If I Didn't Care"
          }
        ],
        "role": "model"
      },
      "finishReason": "STOP",
      "index": 0,
      "safetyRatings": [
        {
          "category": "HARM_CATEGORY_SEXUALLY_EXPLICIT",
          "probability": "NEGLIGIBLE"
        },
        {
          "category": "HARM_CATEGORY_HATE_SPEECH",
          "probability": "NEGLIGIBLE"
        },
        {
          "category": "HARM_CATEGORY_HARASSMENT",
          "probability": "NEGLIGIBLE"
        },
        {
          "category": "HARM_CATEGORY_DANGEROUS_CONTENT",
          "probability": "NEGLIGIBLE"
        }
      ]
    }
  ],
  "usageMetadata": {
    "promptTokenCount": 9,
    "candidatesTokenCount": 6,
    "totalTokenCount": 15
  }
}
```
1. Open a new windom in VSC and create a new project
2. Inside the project and from the terminal we're going to type `npm init` that will create `package.json` and we'll begin installing the packages that we'll need
3. Install the SDK package as mentioned in the Documentation
https://ai.google.dev/gemini-api/docs/get-started/tutorial?lang=node
4. Indisde package.json we're going to add a `"start": "node index.js",` script where we're going to listen to changes or if we want to listen to constant changes, we'll use *nodemon* which we'd need to install using `npm i nodemon`
5. We'll add the `index.js` file and then type `npm run start`
6. Now we can initialize our model
7. Also to keep our API key separated from our files, we'll create an `.env` file and we'll need to install `npm dotenv` to be able to use the file 
```javascript
const { GoogleGenerativeAI } = require('@google/generative-ai');
require('dotenv').config()

// Access your API key as an environment variable (see "Set up your API key" above)
const genAI = new GoogleGenerativeAI(process.env.API_KEY)

const model = genAI.getGenerativeModel({model: "gemini-pro"})

//You can console.log to check that everything is working
console.log(model);
```
We start by writing our small program to get the result int the terminal like so:
```javascript
const { GoogleGenerativeAI } = require('@google/generative-ai');
require('dotenv').config()

const genAI = new GoogleGenerativeAI(process.env.API_KEY)


async function run (){
  const model = genAI.getGenerativeModel({model: "gemini-pro"})
  const prompt = "Write a short poem about resilience"
  const result = await model.generateContent(prompt);
  const response = await result.response
  const text = response.text()
  console.log(text);
}
run()
```
This will return the following output
```
[nodemon] starting `node index.js`
(node:39002) ExperimentalWarning: The Fetch API is an experimental feature. This feature could change at any time
(Use `node --trace-warnings ...` to show where the warning was created)
Through storms that rage and trials that press,
Resilience blooms, an indomitable crest.
Like willows bending, yet refusing to break,
It weathers adversity with strength it will make.

Scars adorn its form, a testament to pain,
Yet within its depths, a spirit that will sustain.
It rises from the ashes, stronger than before,
A beacon of hope, forever to adore.
```

## Using the Text/Image to Text Model
For this model we'll need the fs package `npm i fs` and also 

```
const { GoogleGenerativeAI } = require('@google/generative-ai');
require('dotenv').config()
const fs = require('fs')

const genAI = new GoogleGenerativeAI(process.env.API_KEY)


//convert local file information to a Google Generative Ai file object
function fileToGenerativePart(path, mimeType){
  return {
    inlineData: {
      data: Buffer.from(fs.readFileSync(path)).toString("base64"),
      mimeType
    },
  };
}

async function run () {
  const model = genAI.getGenerativeModel({model: "gemini-pro-vision"})
  
  const prompt = "What's different between these pictures?"
  
  const imageParts = [
    fileToGenerativePart("./image/img1.jpeg", "image/jpeg"),  //Image of a Cat
    fileToGenerativePart("./image/img2.jpeg", "image/jpeg")  //Image of a Pig
  ]
  const result = await model.generateContent([prompt, ...imageParts])
  const response = await result.response;
  const text = response.text()
  console.log(text);
}

run()
```
Running this code, the AI will return the followign text
```
 The first picture is of a cat and the second picture is of a pig. The cat has fur, whiskers, and a tail. The pig has no fur, no whiskers, and no tail. The cat has blue eyes and the pig has brown eyes. The cat is lying down and the pig is standing up.
```
## Text to Chat Model
Create chatbot that will essentially take all the history of your chat previosly in order to take into context your next questions.

We'll initialize the chat by calling start chat and initialize the chay by calling start the chat and then use send message to send a new user message which she'll also append the message and the response to the chat history.

There are two possible options for roles associated with this, we're going to have the user and this is the role which provides the prompt
```javascript
const { GoogleGenerativeAI } = require('@google/generative-ai');
require('dotenv').config()
const fs = require('fs')

const genAI = new GoogleGenerativeAI(process.env.API_KEY)

async function run () {
  const model = genAI.getGenerativeModel({model: "gemini-pro"})
  const chat = model.startChat({
    history: [
      {
        role: "user",
        parts: [{text: "Hello. I have 2 dogs in my house" }],
      },
      {
        role: "model",
        parts: [{text: "Great to meet you. What would you like to know?" }]
      }
    ]
  })
  const msg = "How many paws are in my house?"
  const result = await chat.sendMessage(msg)
  const response = await result.response
  const text = response.text()
  console.log(text) 
}

run()
```
### Text to Embedding
Enbedding is atechnique used to represent information as a list of floting points in an array. With Gemini you can represent text words sentences and blocks of text in a vectorized form making it easier to compare and contrast embeddings. So for example two texts that share a similar subject matter or sentiment should have similar embeddings which can be identified through mathematical comparison techniques sucn as cosign similarity

The following array of numbers represents a word or a sentence and this is how essentially look for terms with similar meaning so similar semantic meaning
```javascript
/*********
 *  Creating Embbedings
 ************************/
async function run () {
  const model = genAI.getGenerativeModel({model: "embedding-001"})
  const text = "The quick brown fox jump over the lazy dog"

  const result = await model.embedContent(text)
  const embedding = result.embedding
  console.log(embedding)
}
run()
```
And returns the following in the terminal
```
{
  values: [
      0.036987893,  -0.037970692,  -0.030560648,     -0.01690209,
     -0.009496136,  -0.023614142,   0.018649986,    -0.021359833,
       0.02058623,   0.017200666,   0.042441625,      0.02317011,
      0.029778615,  -0.005130026,  -0.022591917,     0.034307215,
       0.02569227, 0.00025096955,   0.007870549,    -0.026282817,
        0.0235454,  0.0006386271,   0.006101349,   0.00025870255,
      0.013751433,   -0.05367174,  -0.013227702,   -0.0046372307,
     -0.005526795,   0.019416656,   -0.06410016,     0.003525156,
     -0.032295607,  -0.054180853,  -0.021636892,     -0.04416859,
       0.02176767,    0.06846326,   0.030861266,     0.042003255,
     -0.001954135,   0.020475173,  -0.013972761,      -0.0397927,
       0.06090618,  -0.005264377,   0.017178722,     0.036924545,
      0.006919786,  -0.018909927,   0.031452045,     0.020351563,
      0.037030924, -0.0016725169,  -0.006946485,     -0.05940283,
       0.02007897,   0.016016474,  -0.012800762,     0.016989106,
      0.029636476,   0.026143694,   0.023377312,      0.08673692,
     -0.039219167,  -0.017827112,  -0.015914286,     0.011953163,
      0.050765425,   0.014034564,    -0.0220211,     -0.06207287,
       0.03967931,   0.014832808,  -0.021397399,     -0.09346757,
     -0.036652442,   0.053009838,   0.046747968,      0.06493412,
     0.0064755282,  -0.052256342,  -0.019069092,    -0.020091362,
      -0.07771212,   0.074779235,  -0.053866394,    0.0072451322,
    -0.0006803601,   0.022997301,   -0.03798879,      0.01612809,
      0.034886803, -0.0034217509, -0.0061543267,     0.042238075,
     -0.009231181,  -0.010895418, -0.0065460713, -0.000114556606,
    ... 668 more items
  ]
}

```