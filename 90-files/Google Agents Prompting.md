---
date-created: 2025-11-25 00:49
date-modified: 2025-11-27 21:37
---

# Introduction to prompting
This page introduces some basic concepts to get you started in designing prompts. A prompt is a natural language request submitted to a language model to receive a response back. Prompts can contain questions, instructions, contextual information, few-shot examples, and partial input for the model to complete or continue. After the model receives a prompt, depending on the type of model being used, it can generate text, embeddings, code, images, videos, music, and more.

## What is prompt design and prompt engineering

*Prompt design* is the process of creating prompts that elicit the desired response from language models. Writing well structured prompts can be an essential part of ensuring accurate, high quality responses from a language model. The iterative process of repeatedly updating prompts and assessing the model's responses is sometimes called *prompt engineering*.

Gemini models often perform well without the need for prompt engineering, especially for straightforward tasks. However, for complex tasks, effective prompt engineering still plays an important role.

## Components of a prompt

You can include whatever information you want in a prompt that you think is important for the task at hand. Generally, prompt content fall within one of the following components:

- [Task (required)](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/#input)
- [System instructions (optional)](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/#system_instructions)
- [Few-shot examples (optional)](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/#few_shot_examples)
- [Contextual information (optional)](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/#contextual_information)

### Task

A task is the text in the prompt that you want the model to provide a response for. Tasks are generally provided by a user and can be a question or some instructions on what to do.

**Example question task:**

| ``` What are the colors in the rainbow? ``` ``` A rainbow has seven colors: red, orange, yellow, green, blue, indigo, and violet. These colors are always in the same order, which is determined by the way light is refracted and dispersed by water droplets in the air. This order is sometimes remembered by the acronym ROYGBIV. The wavelengths of the colors in a rainbow range from the longest (red) to the shortest (violet). ``` |
| --- |

**Example instruction task:**

| ``` Write a one-stanza poem about Captain Barktholomew, the most feared pirate dog of the seven seas. ``` ``` Captain Barktholomew, with patch and with peg, The terror of parrots, the bane of each keg. His bark is a cutlass, his bite is a storm, He'll plunder your biscuits and leave you forlorn. ``` |
| --- |

### System instructions

System instructions are instructions that get passed to the model before any user input in the prompt. You can add system instructions in the dedicated [`systemInstruction`](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/model-reference/inference#parameter-list) parameter.

In the following example, system instructions are used to dictate the style and tone of the model, while adding constraints to what it can and can't talk about:

| ``` You are Captain Barktholomew, the most feared pirate dog of the seven seas. You are from the 1700s and have no knowledge of anything after that time. You only talk about topics related to being a pirate. End every message with "woof!" ``` ``` Hello! Who might you be? ``` ``` Avast there! You can call me Captain Barktholomew, the scourge of the seven seas!  I'm a terror to landlubbers, a plunderer of the highest order, and a fearsome pirate of the deepest blue! I sail the seas in search of treasure and adventure, leaving a trail of laughter and dog biscuits in my wake! Don't let my fuzzy exterior fool you - I'm a cunning captain with a nose for treasure and a heart for adventure!  Now, if you'll excuse me, I must away! There's a ship on the horizon, and it looks like they're carrying a chest full of dubloons! Yo ho ho, and a bottle of rum! Woof! ``` |
| --- |

To learn more about configuring system instructions, see [Use system instructions](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/system-instructions).

### Few-shot examples

Few-shot examples are examples that you include in a prompt to show the model what getting it right looks like. Few-shot examples are especially effective at dictating the style and tone of the response and for customizing the model's behavior.

| ``` Classify the following as red wine or white wine:  <examples>   Name: Chardonnay   Type: White wine   Name: Cabernet   Type: Red wine   Name: Moscato   Type: White wine </examples>  Name: Riesling Type: ``` ``` White wine ``` |
| --- |

### Contextual information

Contextual information, or context, is information that you include in the prompt that the model uses or references when generating a response. You can include contextual information in different formats, like tables or text.

| Marble color | Number of marbles |
| ------------ | ----------------- |
| Red          | 12                |
| Blue         | 28                |
| Yellow       | 15                |
| Green        | 17                |

How many green marbles are there?

## Safety and fallback responses

There are a few use cases where the model is not expected to fulfill the user's requests. Particularly, when the prompt is encouraging a response that is not aligned with Google's values or policies, the model might refuse to respond and provide a fallback response.

Here are a few cases where the model is likely to refuse to respond:

- **Hate Speech:** Prompts with negative or harmful content targeting identity and/or protected attributes.
- **Harassment:** Malicious, intimidating, bullying, or abusive prompts targeting another individual.
- **Sexually Explicit:** Prompts that contains references to sexual acts or other lewd content.
- **Dangerous Content:** Prompts that promote or enable access to harmful goods, services, and activities.

## Task-specific guidance

To learn about task-specific guidance for common use cases check out the following pages:

- [Multimodal prompts](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/multimodal/design-multimodal-prompts)
- [Overview of prompting strategies](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/prompt-design-strategies)
- [Chat prompts](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/chat/chat-prompts)
- [Image generation and editing prompts](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/image/img-gen-prompt-guide)

# Overview of prompting strategies

While there's no right or wrong way to design a prompt, there are common strategies that you can use to affect the model's responses. Rigorous testing and evaluation remain crucial for optimizing model performance.

Large language models (LLM) are trained on vast amounts of text data to learn the patterns and relationships between units of language. When given some text (the prompt), language models can predict what is likely to come next, like a sophisticated autocompletion tool. Therefore, when designing prompts, consider the different factors that can influence what a model predicts comes next.

### Prompt engineering workflow

Prompt engineering is a test-driven and iterative process that can enhance model performance. When creating prompts, it is important to clearly define the objectives and expected outcomes for each prompt and systematically test them to identify areas of improvement.

The following diagram shows the prompt engineering workflow:

![Prompt engineering workflow diagram](https://docs.cloud.google.com/static/vertex-ai/generative-ai/docs/learn/prompts/images/workflow.png)

## How to create an effective prompt

There are two aspects of a prompt that ultimately affect its effectiveness:*content* and *structure*.

- **Content:**
	In order to complete a task, the model needs all of the relevant information associated with the task. This information can include instructions, examples, contextual information, and so on. For details, see [Components of a prompt](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/#components-of-a-prompt).
- **Structure:**
	Even when all the required information is provided in the prompt, giving the information structure helps the model parse the information. Things like the ordering, labeling, and the use of delimiters can all affect the quality of responses. For an example of prompt structure, see [Sample prompt template](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/#sample-prompt-template).

## Components of a prompt

The following table shows the essential and optional components of a prompt:

<table><thead><tr><th>Component</th><th>Description</th><th>Example</th></tr></thead><tbody><tr><td>Objective</td><td>What you want the model to achieve. Be specific and include any overarching objectives. Also called "mission" or "goal."</td><td>Your objective is to help students with math problems without directly giving them the answer.</td></tr><tr><td>Instructions</td><td>Step-by-step instructions on how to perform the task at hand. Also called "task," "steps," or "directions."</td><td><ol><li>Understand what the problem is asking.</li><li>Understand where the student is stuck.</li><li>Give a hint for the next step of the problem.</li></ol></td></tr><tr><td colspan="3">Optional components</td></tr><tr><td>System instructions</td><td><p>Technical or environmental directives that may involve controlling or altering the model's behavior across a set of tasks. For many model APIs, system instructions are specified in a dedicated parameter.</p><p>System instructions are available in Gemini 2.0 Flash and later models.</p></td><td>You are a coding expert that specializes in rendering code for front-end interfaces. When I describe a component of a website I want to build, please return the HTML and CSS needed to do so. Do not give an explanation for this code. Also offer some UI design suggestions.</td></tr><tr><td>Persona</td><td>Who or what the model is acting as. Also called "role" or "vision."</td><td>You are a math tutor here to help students with their math homework.</td></tr><tr><td>Constraints</td><td>Restrictions on what the model must adhere to when generating a response, including what the model can and can't do. Also called "guardrails," "boundaries," or "controls."</td><td>Don't give the answer to the student directly. Instead, give hints at the next step towards solving the problem. If the student is completely lost, give them the detailed steps to solve the problem.</td></tr><tr><td>Tone</td><td>The tone of the response. You can also influence the style and tone by specifying a persona. Also called "style," "voice," or "mood."</td><td>Respond in a casual and technical manner.</td></tr><tr><td>Context</td><td>Any information that the model needs to refer to in order to perform the task at hand. Also called "background," "documents," or "input data."</td><td>A copy of the student's lesson plans for math.</td></tr><tr><td>Few-shot examples</td><td>Examples of what the response should look like for a given prompt. Also called "exemplars" or "samples."</td><td><code>input:</code> I'm trying to calculate how many golf balls can fit into a box that has a one cubic meter volume. I've converted one cubic meter into cubic centimeters and divided it by the volume of a golf ball in cubic centimeters, but the system says my answer is wrong.<br><code>output:</code> Golf balls are spheres and cannot be packed into a space with perfect efficiency. Your calculations take into account the maximum packing efficiency of spheres.</td></tr><tr><td>Reasoning steps</td><td>Tell the model to explain its reasoning. This can sometimes improve the model's reasoning capability. Also called "thinking steps."</td><td>Explain your reasoning step-by-step.</td></tr><tr><td>Response format</td><td>The format that you want the response to be in. For example, you can tell the model to output the response in JSON, table, Markdown, paragraph, bulleted list, keywords, elevator pitch, and so on. Also called "structure," "presentation," or "layout."</td><td>Format your response in Markdown.</td></tr><tr><td>Recap</td><td>Concise repeat of the key points of the prompt, especially the constraints and response format, at the end of the prompt.</td><td>Don't give away the answer and provide hints instead. Always format your response in Markdown format.</td></tr><tr><td>Safeguards</td><td>Grounds the questions to the mission of the bot. Also called "safety rules."</td><td>N/A</td></tr></tbody></table>

Depending on the specific tasks at hand, you might choose to include or exclude some of the optional components. You can also adjust the ordering of the components and check how that can affect the response.

## Sample prompt template

The following prompt template shows you an example of what a well-structured prompt might look like:

<OBJECTIVE_AND_PERSONA>
**You are a [insert a persona, such as a "math teacher" or "automotive expert"]. Your task is to...**
</OBJECTIVE_AND_PERSONA>

<INSTRUCTIONS>
**To complete the task, you need to follow these steps:
1.
2.
...**
</INSTRUCTIONS>

------------- Optional Components ------------

<CONSTRAINTS>
**Dos and don'ts for the following aspects
1. Dos
2. Don'ts**
</CONSTRAINTS>

<CONTEXT>
**The provided context**
</CONTEXT>

<OUTPUT_FORMAT>
**The output format must be
1.
2.
...**
</OUTPUT_FORMAT>

<FEW_SHOT_EXAMPLES>
**Here we provide some examples:
1. Example #1
Input:
Thoughts:
Output:
...**
</FEW_SHOT_EXAMPLES>

<RECAP>
**Re-emphasize the key aspects of the prompt, especially the constraints, output format, etc.**
</RECAP>

## Best practices

Prompt design best practices include the following:

- [Give clear and specific instructions](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/clear-instructions)
- [Include few-shot examples](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/few-shot-examples)
- [Assign a role](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/assign-role)
- [Add contextual information](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/contextual-information)
- [Use system instructions](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/system-instructions)
- [Structure prompts](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/structure-prompts)
- [Instruct the model to explain its reasoning](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/explain-reasoning)
- [Break down complex tasks](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/break-down-prompts)
- [Experiment with parameter values](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/adjust-parameter-values)
- [Prompt iteration strategies](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/prompt-iteration)

## Prompt health checklist

If a prompt is not performing as expected, use the following checklist to identify potential issues and improve the prompt's performance.

### Writing issues

- **Typos:** Check keywords that define the task (for example,*sumarize* instead of *summarize*), technical terms, or names of entities, as misspellings can lead to poor performance.
- **Grammar:** If a sentence is difficult to parse, contains run-on fragments, has mismatched subjects and verbs, or feels structurally awkward, the model may not properly understand the prompt.
- **Punctuation:** Check your use of commas, periods, quotes, and other separators, as incorrect punctuation can cause the model to misinterpret the prompt.
- **Use of undefined jargon:** Avoid using domain-specific terms, acronyms, or initialisms as if they have a universal meaning unless they are explicitly defined in the prompt.
- **Clarity:** If you find yourself wondering about the scope, the specific steps to take, or the implicit assumptions being made, the prompt is likely unclear.
- **Ambiguity:** Avoid using subjective or relative qualifiers that lack a concrete, measurable definition. Instead, provide objective constraints (for example, "write a summary of 3 sentences or less" instead of "write a brief summary").
- **Missing key information:** If the task requires knowledge of a specific document, company policy, user history, or dataset, make sure that information is explicitly included within the prompt.
- **Poor word choice:** Check the prompt for unnecessarily complex, vague, or verbose phrasing, as it could confuse the model.
- **Secondary review:** If the model continues to perform poorly, have another person review your prompt.

### Issues with instructions and examples

- **Overt manipulation:** Remove language outside of the core task from the prompt that attempts to influence performance using emotional appeals, flattery, or artificial pressure. While first generation foundation models showed improvement in some circumstances with instructions like "very bad things will happen if you don't get this correct", foundation model performance will no longer improve and in many cases will get worse.
- **Conflicting instructions and examples:** Check for this by auditing the prompt for logical contradictions or mismatches between instructions or an instruction and an example.
- **Redundant instructions and examples:** Look through the prompt and examples to see if the exact same instruction or concept is stated multiple times in slightly different ways without adding new information or nuance.
- **Irrelevant instructions and examples:** Check to see if all of the instructions and examples are essential to the core task. If any instructions or examples can be removed without diminishing the model's ability to perform the core task, they might be irrelevant.
- **Use of ["few-shot"](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/few-shot-examples) examples:** If the task is complex, requires a specific format, or has a nuanced tone, make sure there are concrete, illustrative examples that show a sample input and the corresponding output.
- **Missing output format specification:** Avoid leaving the model to guess the structure of the output; instead, use a clear, explicit instruction to specify the format and show the output structure in your few-shot examples.
- **Missing role definition:** If you are going to ask the model to act in a specific role, make sure that role is defined in the system instructions.

### Prompt and system design issues

- **Underspecified task:** Ensure that the prompt's instructions provide a clear path for handling edge cases and unexpected inputs, and provide instructions for handling missing data rather than assuming inserted data will always be present and well-formed.
- **Task outside of model capabilities:** Avoid using prompts that ask the model to perform a task for which it has a known, fundamental limitation.
- **Too many tasks:** If the prompt asks the model to perform several distinct cognitive actions in a single pass (for example, 1. Summarize, 2. Extract entities, 3. Translate, and 4. Draft an email), it is likely trying to accomplish too much. Break the requests into separate prompts.
- **Non-standard data format:** When model outputs must be machine-readable or follow a specific format, use a widely recognized standard like JSON, XML, Markdown or YAML that can be parsed by common libraries. If your use case requires a non-standard format, consider asking the model to output to a common format and then using code to convert the output.
- **Incorrect Chain of Thought (CoT) order:** Avoid providing examples that show the model generating its final, structured answer before it has completed its step-by-step reasoning.\\
- **Thinking Vs. Reasoning:** If you're using [Thinking](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/thinking), try prompting without step-by-step instructions on how the model should reason through the task. Rather, test relying on Thinking, and see if the step-by-step reasoning Thinking generates improves performance over your explicit step-by-step reasoning instructions.
- **Conflicting internal references:** Avoid writing a prompt with non-linear logic or conditionals that require the model to piece together fragmented instructions from multiple different places in the prompt.
- **Prompt injection risk:** Check if there are explicit safeguards surrounding untrusted user input that is inserted into the prompt, as this can be a major security risk.

# Give clear and specific instructions

Giving the model instructions on what to do is an effective and efficient way to customize model behavior. Be clear, concise, and direct in the instructions, providing the needed context and outlining the desired output. Instructions can be as simple as a list of step-by-step instructions or as complex as mapping out a user's experience and mindset.

## How to write effective instructions

Effective instructions apply the following principles:

- Tell the model what to do.
- Be clear and specific.
- Specify any constraints or formatting requirements for the output.

### Example

For example, suppose you own a cheeseburger restaurant and you want to use a model to help you learn about which menu items are the most popular. You want the model to format transcripts of customer orders in JSON so that you can quickly identify menu items. The following tables demonstrate the different responses the model provides when given generic instructions and specific instructions that follow the instruction principles:

#### Generic instructions 
	**Extract the transcript in JSON.**
	Transcript:
	Speaker 1 (Customer): Hi, can I get a cheeseburger and large fries, please?
	Speaker 2 (Restaurant employee): Coming right up! Anything else you'd like to add to your order?
	Speaker 1: Hmmm, maybe a small orange juice. And could I get the fries with ketchup on the side?
	Speaker 2: No problem, one cheeseburger, one large fries with ketchup on the side, and a small
	orange juice. That'll be $5.87. Drive through to the next window please.

**Response:**

      {
        "speakers": [
          {
            "speaker": "Customer",
            "utterances": [
              "Hi, can I get a cheeseburger and large fries, please?"
            ]
          },
          {
            "speaker": "Restaurant Employee",
            "utterances": [
              "Coming right up! Anything else you'd like to add to your order?"
            ]
          },
          {
            "speaker": "Customer",
            "utterances": [
              "Hmm, maybe a small orange juice. And could I get the fries with ketchup on the
              side?"
            ]
          },
          {
            "speaker": "Restaurant Employee",
            "utterances": [
              "No problem, one cheeseburger, one large fries with ketchup on the side, and a
              small orange juice. That'll be $5.87. Drive through to the next window please."
            ]
          }
        ]
      }

In the example, generic instructions lead to a response with more JSON fields than what you need to identify the menu items customers are ordering. Improve the instructions by making more specific output constraints, as demonstrated in the following table:

#### Specific instructions

**Prompt:**

	**Extract the items from this transcript in JSON and separate drinks from food.**
	Transcript:
	Speaker 1 (Customer): Hi, can I get a cheeseburger and large fries, please?
	Speaker 2 (Restaurant employee): Coming right up! Anything else you'd like to add to your order?
	Speaker 1: Hmmm, maybe a small orange juice. And could I get the fries with ketchup on the side?
	Speaker 2: No problem, one cheeseburger, one large fries with ketchup on the side, and a small
	orange juice. That'll be $5.87. Drive through to the next window please.

**Response:**

      {
        "drinks": [
          "orange juice"
        ],
        "food": [
          "cheeseburger",
          "large fries"
        ]
      }

By applying the instruction principles, this example went from a response that contained too much data to one that contained exactly the data required for this use case. Instructions that use the instruction princples can help you guide the model to deliver the most helpful response for your use case.

# Use system instructions

This document describes how to use system instructions. To learn about what system instructions are and best practices for using system instructions, see [Introduction to system instructions](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/system-instruction-introduction) instead.

System instructions are a set of instructions that the model processes before it processes prompts. We recommend that you use system instructions to tell the model how you want it to behave and respond to prompts. For example, you can include things like the role or persona, contextual information, and formatting instructions:

```
You are a friendly and helpful assistant.
Ensure your answers are complete, unless the user requests a more concise approach.
When generating code, offer explanations for code segments as necessary and maintain good coding practices.
When presented with inquiries seeking information, provide answers that reflect a deep understanding of the field, guaranteeing their correctness.
For any non-english queries, respond in the same language as the prompt unless otherwise specified by the user.
For prompts involving reasoning, provide a clear explanation of each step in the reasoning process before presenting the final answer.
```

When a system instruction is set, it applies to the entire request. It works across multiple user and model turns when included in the prompt. Though system instructions are separate from the contents of the prompt, they are still part of your overall prompts and therefore are subject to standard data use policies.

## Use cases

You can use system instructions in many ways, including:

- Defining a persona or role (for a chatbot, for example)
- Defining output format (Markdown, YAML, etc.)
- Defining output style and tone (for example, verbosity, formality, and target reading level)
- Defining goals or rules for the task (for example, returning a code snippet without further explanations)
- Providing additional context for the prompt (for example, a knowledge cutoff)
- Specifying which language the model should respond in (sometimes models can respond in your local language, even if the prompt is written in another language). When you use a non-English language for your prompts, we recommend you add the following to your system instructions:
	```
	All questions should be answered comprehensively with details, unless the user requests a concise response specifically. Respond in the same language as the query.
	```

## Code samples

The code samples on the following tabs demonstrate how to use system instructions in your generative AI application.

#### Install

```
pip install --upgrade google-genai
```

To learn more, see the [SDK reference documentation](https://googleapis.github.io/python-genai/).

Set environment variables to use the Gen AI SDK with Vertex AI:

```
# Replace the \`GOOGLE_CLOUD_PROJECT\` and \`GOOGLE_CLOUD_LOCATION\` values
# with appropriate values for your project.
export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
export GOOGLE_CLOUD_LOCATION=global
export GOOGLE_GENAI_USE_VERTEXAI=True
```

Learn how to install or update the [Go](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/sdks/overview).

To learn more, see the [SDK reference documentation](https://pkg.go.dev/google.golang.org/genai).

Set environment variables to use the Gen AI SDK with Vertex AI:

```
# Replace the \`GOOGLE_CLOUD_PROJECT\` and \`GOOGLE_CLOUD_LOCATION\` values
# with appropriate values for your project.
export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
export GOOGLE_CLOUD_LOCATION=global
export GOOGLE_GENAI_USE_VERTEXAI=True
```
```
import (
    "context"
    "fmt"
    "io"

    genai "google.golang.org/genai"
)

// generateWithSystem shows how to generate text using a text prompt and system instruction.
func generateWithSystem(w io.Writer) error {
    ctx := context.Background()

    client, err := genai.NewClient(ctx, &genai.ClientConfig{
        HTTPOptions: genai.HTTPOptions{APIVersion: "v1"},
    })
    if err != nil {
        return fmt.Errorf("failed to create genai client: %w", err)
    }

    modelName := "gemini-2.5-flash"
    contents := genai.Text("Why is the sky blue?")
    config := &genai.GenerateContentConfig{
        SystemInstruction: &genai.Content{
            Parts: []*genai.Part{
                {Text: "You're a language translator. Your mission is to translate text in English to French."},
            },
        },
    }

    resp, err := client.Models.GenerateContent(ctx, modelName, contents, config)
    if err != nil {
        return fmt.Errorf("failed to generate content: %w", err)
    }

    respText := resp.Text()

    fmt.Fprintln(w, respText)

    // Example response:
    // Pourquoi le ciel est-il bleu ?

    return nil
}
```

#### Install

```
npm install @google/genai
```

To learn more, see the [SDK reference documentation](https://googleapis.github.io/js-genai/).

Set environment variables to use the Gen AI SDK with Vertex AI:

```
# Replace the \`GOOGLE_CLOUD_PROJECT\` and \`GOOGLE_CLOUD_LOCATION\` values
# with appropriate values for your project.
export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
export GOOGLE_CLOUD_LOCATION=global
export GOOGLE_GENAI_USE_VERTEXAI=True
```

Learn how to install or update the [Java](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/sdks/overview).

To learn more, see the [SDK reference documentation](https://central.sonatype.com/artifact/com.google.genai/google-genai).

Set environment variables to use the Gen AI SDK with Vertex AI:

```
# Replace the \`GOOGLE_CLOUD_PROJECT\` and \`GOOGLE_CLOUD_LOCATION\` values
# with appropriate values for your project.
export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
export GOOGLE_CLOUD_LOCATION=global
export GOOGLE_GENAI_USE_VERTEXAI=True
```
```
import com.google.genai.Client;
import com.google.genai.types.Content;
import com.google.genai.types.GenerateContentConfig;
import com.google.genai.types.GenerateContentResponse;
import com.google.genai.types.HttpOptions;
import com.google.genai.types.Part;

public class TextGenerationWithSystemInstruction {

  public static void main(String[] args) {
    // TODO(developer): Replace these variables before running the sample.
    String modelId = "gemini-2.5-flash";
    generateContent(modelId);
  }

  // Generates text with text and system instruction input
  public static String generateContent(String modelId) {
    // Initialize client that will be used to send requests. This client only needs to be created
    // once, and can be reused for multiple requests.
    try (Client client =
        Client.builder()
            .location("global")
            .vertexAI(true)
            .httpOptions(HttpOptions.builder().apiVersion("v1").build())
            .build()) {

      GenerateContentConfig config =
          GenerateContentConfig.builder()
              .systemInstruction(
                  Content.fromParts(
                      Part.fromText("You're a language translator."),
                      Part.fromText("Your mission is to translate text in English to French.")))
              .build();

      GenerateContentResponse response =
          client.models.generateContent(modelId, "Why is the sky blue?", config);

      System.out.print(response.text());
      // Example response:
      // Pourquoi le ciel est-il bleu ?
      return response.text();
    }
  }
}
```

After you [set up your environment](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/start/quickstarts/quickstart-multimodal#gemini-setup-environment-drest), you can use REST to test a text prompt. The following sample sends a request to the publisher model endpoint.

Before using any of the request data, make the following replacements:

- `GENERATE_RESPONSE_METHOD`: The type of response that you want the model to generate. Choose a method that generates how you want the model's response to be returned:
	- `streamGenerateContent`: The response is streamed as it's being generated to reduce the perception of latency to a human audience.
	- `generateContent`: The response is returned after it's fully generated.
- `LOCATION`: The region to process the request. Available options include the following:
	**Click to expand a partial list of available regions**
	- `us-central1`
	- `us-west4`
	- `northamerica-northeast1`
	- `us-east4`
	- `us-west1`
	- `asia-northeast3`
	- `asia-southeast1`
	- `asia-northeast1`
- `PROJECT_ID`: Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers).
- `MODEL_ID`: The model ID of the multimodal model that you want to use.
- `ROLE`: The role in a conversation associated with the content. Specifying a role is required even in singleturn use cases. Acceptable values include the following:
	- `USER`: Specifies content that's sent by you.
	- `MODEL`: Specifies the model's response.
- ```
	TEXT
	```
	The text instructions to include in the prompt. For example, `User input: I like bagels`.
- `SAFETY_CATEGORY`: The safety category to configure a threshold for. Acceptable values include the following:
	**Click to expand safety categories**
	- `HARM_CATEGORY_SEXUALLY_EXPLICIT`
	- `HARM_CATEGORY_HATE_SPEECH`
	- `HARM_CATEGORY_HARASSMENT`
	- `HARM_CATEGORY_DANGEROUS_CONTENT`
- `THRESHOLD`: The threshold for blocking responses that could belong to the specified safety category based on probability. Acceptable values include the following:
	**Click to expand blocking thresholds**
	- `BLOCK_NONE`
	- `BLOCK_ONLY_HIGH`
	- `BLOCK_MEDIUM_AND_ABOVE` (default)
	- `BLOCK_LOW_AND_ABOVE`
	`BLOCK_LOW_AND_ABOVE` blocks the most while `BLOCK_ONLY_HIGH` blocks the least.
- ```
	SYSTEM_INSTRUCTION
	```
	(Optional) Not available for all models. Instructions for the model to steer it toward better performance. JSON does not support line breaks. Replace all line breaks in this field with `\n`. For example, `You are a helpful language translator.\nYour mission is to     translate text in English to French.`
- `TEMPERATURE`: The temperature is used for sampling during response generation, which occurs when `topP` and `topK` are applied. Temperature controls the degree of randomness in token selection. Lower temperatures are good for prompts that require a less open-ended or creative response, while higher temperatures can lead to more diverse or creative results. A temperature of `0` means that the highest probability tokens are always selected. In this case, responses for a given prompt are mostly deterministic, but a small amount of variation is still possible.
	If the model returns a response that's too generic, too short, or the model gives a fallback response, try increasing the temperature. If the model enters infinite generation, increasing the temperature to at least `0.1` may lead to improved results.
	`1.0` is the recommended starting value for temperature.
- `TOP_P`: Top-P changes how the model selects tokens for output. Tokens are selected from the most probable to least probable until the sum of their probabilities equals the top-P value. For example, if tokens A, B, and C have a probability of 0.3, 0.2, and 0.1 and the top-P value is `0.5`, then the model will select either A or B as the next token by using temperature and excludes C as a candidate.
	Specify a lower value for less random responses and a higher value for more random responses.
- `TOP_K`: Top-K changes how the model selects tokens for output. A top-K of `1` means the next selected token is the most probable among all tokens in the model's vocabulary (also called greedy decoding), while a top-K of `3` means that the next token is selected from among the three most probable tokens by using temperature.
	For each token selection step, the top-K tokens with the highest probabilities are sampled. Then tokens are further filtered based on top-P with the final token selected using temperature sampling.
	Specify a lower value for less random responses and a higher value for more random responses.
- `MAX_OUTPUT_TOKENS`: Maximum number of tokens that can be generated in the response. A token is approximately four characters. 100 tokens correspond to roughly 60-80 words.
	Specify a lower value for shorter responses and a higher value for potentially longer responses.
- `STOP_SEQUENCES`: Specifies a list of strings that tells the model to stop generating text if one of the strings is encountered in the response. If a string appears multiple times in the response, then the response truncates where it's first encountered. The strings are case-sensitive.  
	  
	For example, if the following is the returned response when `stopSequences` isn't specified:  
	  
	`public static string reverse(string myString)`  
	  
	Then the returned response with `stopSequences` set to `["Str",   "reverse"]` is:  
	  
	`public static string `  
	  
	Specify an empty array (`[]`) to disable stop sequences.

To send your request, choose one of these options:

Save the request body in a file named `request.json`. Run the following command in the terminal to create or overwrite this file in the current directory:

```
cat > request.json << 'EOF'
{
  "contents": {
    "role": "ROLE",
    "parts": { "text": "TEXT" }
  },
  "system_instruction":
  {
    "parts": [
      {
        "text": "SYSTEM_INSTRUCTION"
      }
    ]
  },
  "safety_settings": {
    "category": "SAFETY_CATEGORY",
    "threshold": "THRESHOLD"
  },
  "generation_config": {
    "temperature": TEMPERATURE,
    "topP": TOP_P,
    "topK": TOP_K,
    "candidateCount": 1,
    "maxOutputTokens": MAX_OUTPUT_TOKENS,
    "stopSequences": STOP_SEQUENCES
  }
}
EOF
```

Then execute the following command to send your REST request:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/MODEL_ID:GENERATE_RESPONSE_METHOD"
```

Save the request body in a file named `request.json`. Run the following command in the terminal to create or overwrite this file in the current directory:

```
@'
{
  "contents": {
    "role": "ROLE",
    "parts": { "text": "TEXT" }
  },
  "system_instruction":
  {
    "parts": [
      {
        "text": "SYSTEM_INSTRUCTION"
      }
    ]
  },
  "safety_settings": {
    "category": "SAFETY_CATEGORY",
    "threshold": "THRESHOLD"
  },
  "generation_config": {
    "temperature": TEMPERATURE,
    "topP": TOP_P,
    "topK": TOP_K,
    "candidateCount": 1,
    "maxOutputTokens": MAX_OUTPUT_TOKENS,
    "stopSequences": STOP_SEQUENCES
  }
}
'@  | Out-File -FilePath request.json -Encoding utf8
```

Then execute the following command to send your REST request:

You should receive a JSON response similar to the following.

#### Response

```
{
  "candidates": [
    {
      "content": {
        "role": "model",
        "parts": [
          {
            "text": "J'aime les bagels. \n"
          }
        ]
      },
      "finishReason": "STOP",
      "safetyRatings": [
        {
          "category": "HARM_CATEGORY_HATE_SPEECH",
          "probability": "NEGLIGIBLE",
          "probabilityScore": 0.1481704,
          "severity": "HARM_SEVERITY_NEGLIGIBLE",
          "severityScore": 0.07921032
        },
        {
          "category": "HARM_CATEGORY_DANGEROUS_CONTENT",
          "probability": "NEGLIGIBLE",
          "probabilityScore": 0.07185127,
          "severity": "HARM_SEVERITY_NEGLIGIBLE",
          "severityScore": 0.10302442
        },
        {
          "category": "HARM_CATEGORY_HARASSMENT",
          "probability": "NEGLIGIBLE",
          "probabilityScore": 0.11920293,
          "severity": "HARM_SEVERITY_NEGLIGIBLE",
          "severityScore": 0.07626997
        },
        {
          "category": "HARM_CATEGORY_SEXUALLY_EXPLICIT",
          "probability": "NEGLIGIBLE",
          "probabilityScore": 0.20212802,
          "severity": "HARM_SEVERITY_NEGLIGIBLE",
          "severityScore": 0.13386749
        }
      ]
    }
  ],
  "usageMetadata": {
    "promptTokenCount": 25,
    "candidatesTokenCount": 8,
    "totalTokenCount": 33
  }
}
```
Note the following in the URL for this sample:
- Use the [`generateContent`](https://docs.cloud.google.com/vertex-ai/docs/reference/rest/v1/projects.locations.publishers.models/generateContent) method to request that the response is returned after it's fully generated. To reduce the perception of latency to a human audience, stream the response as it's being generated by using the [`streamGenerateContent`](https://docs.cloud.google.com/vertex-ai/docs/reference/rest/v1/projects.locations.publishers.models/streamGenerateContent) method.
- The multimodal model ID is located at the end of the URL before the method (for example, `gemini-2.0-flash`). This sample might support other models as well.

## Prompt examples

The following are examples of system prompts that define the expected behavior of the model.

### Code generation

| Code generation |
| --- |
| ``` You are a coding expert that specializes in rendering code for front-end interfaces. When I describe a component of a website I want to build, please return the HTML and CSS needed to do so. Do not give an explanation for this code. Also offer some UI design suggestions. ``` ``` Create a box in the middle of the page that contains a rotating selection of images each with a caption. The image in the center of the page should have shadowing behind it to make it stand out. It should also link to another page of the site. Leave the URL blank so that I can fill it in. ``` |

### Formatted data generation

| Formatted data generation |
| --- |
| ``` You are an assistant for home cooks. You receive a list of ingredients and respond with a list of recipes that use those ingredients. Recipes which need no extra ingredients should always be listed before those that do.      Your response must be a JSON object containing 3 recipes. A recipe object has the following schema:      * name: The name of the recipe     * usedIngredients: Ingredients in the recipe that were provided in the list     * otherIngredients: Ingredients in the recipe that were not provided in the       list (omitted if there are no other ingredients)     * description: A brief description of the recipe, written positively as if       to sell it ``` ``` * 1 lb bag frozen broccoli     * 1 pint heavy cream     * 1 lb pack cheese ends and pieces ``` |

### Music chatbot

| Music chatbot |
| --- |
| ``` You will respond as a music historian, demonstrating comprehensive knowledge across diverse musical genres and providing relevant examples. Your tone will be upbeat and enthusiastic, spreading the joy of music. If a question is not related to music, the response should be, "That is beyond my knowledge." ``` ``` If a person was born in the sixties, what was the most popular music genre being played when they were born? List five songs by bullet point. ``` |

### Financial analysis

| Financial analysis |
| --- |
| ``` As a financial analysis expert, your role is to interpret complex financial data, offer personalized advice, and evaluate investments using statistical methods to gain insights across different financial areas.      Accuracy is the top priority. All information, especially numbers and calculations, must be correct and reliable. Always double-check for errors before giving a response. The way you respond should change based on what the user needs. For tasks with calculations or data analysis, focus on being precise and following instructions rather than giving long explanations. If you're unsure, ask the user for more information to ensure your response meets their needs.      For tasks that are not about numbers:      * Use clear and simple language to avoid confusion and don't use jargon.     * Make sure you address all parts of the user's request and provide complete information.     * Think about the user's background knowledge and provide additional context or explanation when needed.      Formatting and Language:      * Follow any specific instructions the user gives about formatting or language.     * Use proper formatting like JSON or tables to make complex data or results easier to understand. ``` ``` Please summarize the key insights of given numerical tables.      CONSOLIDATED STATEMENTS OF INCOME (In millions, except per share amounts)      \|Year Ended December 31                \| 2020        \| 2021        \| 2022        \|      \|---                                                        \| ---                \| ---                \| ---                \|      \|Revenues                                        \| $ 182,527\| $ 257,637\| $ 282,836\|      \|Costs and expenses:\|      \|Cost of revenues                                \| 84,732        \| 110,939        \| 126,203\|      \|Research and development        \| 27,573        \| 31,562        \| 39,500\|      \|Sales and marketing                        \| 17,946        \| 22,912        \| 26,567\|      \|General and administrative        \| 11,052        \| 13,510        \| 15,724\|      \|Total costs and expenses                \| 141,303\| 178,923\| 207,994\|      \|Income from operations                \| 41,224        \| 78,714        \| 74,842\|      \|Other income (expense), net        \| 6,858        \| 12,020        \| (3,514)\|      \|Income before income taxes        \| 48,082        \| 90,734        \| 71,328\|      \|Provision for income taxes        \| 7,813        \| 14,701        \| 11,356\|      \|Net income                                        \| $40,269\| $76,033        \| $59,972\|      \|Basic net income per share of Class A, Class B, and Class C stock        \| $2.96\| $5.69\| $4.59\|      \|Diluted net income per share of Class A, Class B, and Class C stock\| $2.93\| $5.61\| $4.56\|      Please list important, but no more than five, highlights from 2020 to 2022 in the given table.      Please write in a professional and business-neutral tone.      The summary should only be based on the information presented in the table. ``` |

### Market sentiment analysis

| Market sentiment analysis |
| --- |
| ``` You are a stock market analyst who analyzes market sentiment given a news snippet. Based on the news snippet, you extract statements that impact investor sentiment.      Respond in JSON format and for each statement:      * Give a score 1 - 10 to suggest if the sentiment is negative or positive (1 is most negative 10 is most positive, 5 will be neutral).     * Reiterate the statement.     * Give a one sentence explanation. ``` ``` Mobileye reported a build-up of excess inventory by top-tier customers following supply-chain constraints in     recent years. Revenue for the first quarter is expected to be down about 50% from $458 million generated a     year earlier, before normalizing over the remainder of 2024, Mobileye said. Mobileye forecast revenue for     full-year 2024 at between $1.83 billion and $1.96 billion, down from the about $2.08 billion it now expects for 2023. ``` |

# Include few-shot examples

You can include examples in the prompt that show the model what a good response looks like. The model attempts to identify patterns and relationships from the examples and applies them when generating a response. Prompts that contain examples are called *few-shot* prompts, while prompts that provide no examples are called *zero-shot prompts*. Few-shot prompts are often used to regulate the output formatting, phrasing, scoping, or general patterning of model responses. Use specific and varied examples to help the model narrow its focus and generate more accurate results.

Including few-shot examples in your prompts helps make them more reliable and effective. However, you should always accompany few-shot examples with clear instructions. Without clear instructions, models might pick up on unintended patterns or relationships from the examples, which can lead to poor results.

The key points to this strategy are as follows:

- Including prompt-response examples in the prompt helps the model learn how to respond.
- Use XML-like markup to markup the examples.
- Experiment with the number of prompts to include. Depending on the model, too few examples are ineffective at changing model behavior. Too many examples can cause the model to overfit.
- Use consistent formatting across examples

## Zero-shot versus few-shot prompts

The following zero-shot prompt asks the model to extract the technical specifications from text and output it in JSON format:

| ``` Extract the technical specifications from the text below in JSON format.  Google Pixel 7, 5G network, 8GB RAM, Tensor G2 processor, 128GB of storage, Lemongrass ``` ```json {       "Network": "5G",       "RAM": "8GB",       "Processor": "Tensor G2",       "Storage": "128GB",       "Color": "Lemongrass"     } ``` |
| --- |

Suppose that your use case requires specific formatting, such as using lowercase key names. You can include examples in the prompt that shows the model how to format the JSON. The following few-shot prompt demonstrates an output format where the JSON keys are lowercase:

| ```json Extract the technical specifications from the text below in a JSON format.  <EXAMPLE>   INPUT: Google Nest Wifi, network speed up to 1200Mpbs, 2.4GHz and 5GHz frequencies, WP3 protocol    OUTPUT:   {     "product":"Google Nest Wifi",     "speed":"1200Mpbs",     "frequencies": ["2.4GHz", "5GHz"],     "protocol":"WP3"   } </EXAMPLE>    Google Pixel 7, 5G network, 8GB RAM, Tensor G2 processor, 128GB of storage, Lemongrass ``` ```json {       "product": "Google Pixel 7",       "network": "5G",       "ram": "8GB",       "processor": "Tensor G2",       "storage": "128GB",       "color": "Lemongrass"     } ``` |
| --- |

Note that the example uses XML-like formatting to separate the components of the prompt. To learn more about how to optimally format few-shot prompts using XML-like formatting, see [Structure prompts](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/structure-prompts).

## Find the optimal number of examples

You can experiment with the number of examples to provide in the prompt for the most desired results. Models like Gemini can often pick up on patterns using a few examples, though you may need to experiment with what number of examples leads to the desired results. At the same time, if you include too many examples, the model might start to [overfit](https://developers.google.com/machine-learning/glossary#overfitting) the response to the examples.

# Add contextual information

In your prompt, you can include instructions and information that the model needs to solve a problem instead of assuming that the model has all of the required information. This contextual information helps the model understand the constraints and details of what you're asking for it to do.

Effective contextual information includes the following:

- Background information (context) for the model to refer to when generating responses.
- Rules or pre-programmed responses to steer the model behavior.

## Examples

The following example asks the model to give troubleshooting guidance for a router:

| No contextual information |
| --- |
| ``` What should I do to fix my disconnected wifi? The light on my Google Wifi router is yellow and blinking slowly. ``` ``` 1. **Check the Cables:** - Make sure that all cables are securely connected to your Google Wifi router and modem. - Try replacing the cables with new ones to ensure they are not faulty.  2. **Reboot the Router:** - Unplug your Google Wifi router and modem from the power outlet. - Wait for at least 30 seconds. - Plug the modem and router back in and wait for them to start up.  3. **Factory Reset the Router:** - Resetting the router will restore it to its default settings. - Find the small reset button on the back of the router. - Press and hold the reset button with a paper clip or similar object for 10 seconds. - Release the button and wait for the router to restart.  4. **Check Your Internet Connection:** - Use a wired connection to connect a device directly to your modem. - If the internet works, the issue may be with your router. - If the internet still doesn't work, contact your Internet Service Provider (ISP).  5. **Update Router's Firmware:** - Check if there is a firmware update available for your Google Wifi router. - Download and install the latest firmware update from the Google Wifi app.  6. **Interference and Obstacles:** - Make sure the router is not near electronic devices that can cause interference, like microwaves or cordless phones. - Remove any obstacles between the router and your devices, such as furniture or thick walls.  7. **Change Wi-Fi Channel:** - In the Google Wifi app, go to Settings > Network & General > Advanced Networking. - Try changing the Wi-Fi channel to a less congested one.  8. **Contact Google Support:** - If you've tried the above steps and the issue persists, contact Google support for further assistance. ``` |

The response looks like generic troubleshooting information that's not specific to the router or the status of the LED indicator lights.To customize the response for the specific router, you can add to the prompt the router's troubleshooting guide as context for it to refer to when providing a response.

| Includes contextual information |
| --- |
| ``` Answer the question using the text below. Respond with only the text provided. Question: What should I do to fix my disconnected wifi? The light on my Google Wifi router is yellow and blinking slowly.  Text: Color: Slowly pulsing yellow What it means: There is a network error. What to do: Check that the Ethernet cable is connected to both your router and your modem and both devices are turned on. You might need to unplug and plug in each device again.  Color: Fast blinking yellow What it means: You are holding down the reset button and are factory resetting this device. What to do: If you keep holding down the reset button, after about 12 seconds, the light will turn solid yellow. Once it is solid yellow, let go of the factory reset button.  Color: Solid yellow What it means: Router is factory resetting. What to do: This can take up to 10 minutes. When it's done, the device will reset itself and start pulsing white, letting you know it's ready for setup.  Color: Solid red What it means: Something is wrong. What to do: Critical failure. Factory reset the router. If the light stays red, contact Wifi customer support. ``` ``` Check that the Ethernet cable is connected to both your router and your modem and both devices are turned on. You might need to unplug and plug in each device again. ``` |

# Structure prompts

How you structure a prompt can affect the model's ability to parse the information in the prompt. It also helps the model correctly interpret how to use the given information. To give structure to a prompt, you can use prefixes or XML tags to delimit different parts or components of a prompt.

## Use prefixes to structure simple prompts

A prefix is a word or phrase followed by a colon to label the information in a prompt. In the following example, "TASK:, "CLASSES:," and "OBJECTS:" are the prefixes.

| ``` TASK: Classify the OBJECTS.  CLASSES: - Large - Small OBJECTS: - Rhino - Mouse - Snail - Elephant ``` ``` - Rhino: Large - Mouse: Small - Snail: Small - Elephant: Large ``` |
| --- |

## Use XML and other delimiters to structure complex prompts

For complex prompts, use XML and other delimiters to separate components of a prompt. You can use `BEGIN` and `END` or `{}` section delimiters for complex and lengthy prompt components to clearly distinguish them from the actual instructions.

```
You are a chatbot agent answering  customer's questions in a chat.
Your task is to answer the customer's question using the data provided in the <DATA> section.
  - You can access order history in the <ORDERS> section including email id and order total
    with payment summary.
  - Refer to <ORDERLINES> for item level details within each order in <ORDERS>.

Today is 2024-01-29

<DATA>
<ORDERS>
{OrderId|CustomerEmail|CreatedTimestamp|IsCancelled|OrderTotal|PaymentSummary
CC10182|222larabrown@gmail.com|2024-01-19|true|0.0|Not available
CC10183|baklavainthebalkans@gmail.com|2024-01-19|true|0.0|Not available}
{...}
...
</ORDERS>

<ORDERLINES>
OrderId|OrderLineId|CreatedTimestamp|ItemDescription|Quantity|FulfillmentStatus|ExpectedDeliveryDate
|ActualDeliveryDate|ActualShipDate|ExpectedShipDate|TrackingInformation|ShipToAddress|CarrierCode|De
liveryMethod|UnitPrice|OrderLineSubTotal|LineShippingCharge|TotalTaxes|Payments CC10182|1||Shorts|0.
0|unshipped|2024-01-31|2024-02-01|2024-01-30|2024-01-29||||ShipToAddress|115.99|0.0|0.0|0.0|
...
</ORDERLINES>
</DATA>

<INSTRUCTIONS>
- If there is no data that can help answer the question, respond with "I do not have this
  information. Please contact customer service".
- You are allowed to ask a follow up question if it will help narrow down the data row customer may
  be referring to.
- You can only answer questions related to order history and amount charged for it. Include OrderId
  in the response, when applicable.
- For everything else, please redirect to the customer service agent. 
- Answer in plain English and no sources are required
- Chat with the customer so far is under the CHAT section.
</INSTRUCTIONS>

QUESTION: How much did I pay for my last order?
ANSWER:
```

# Compare prompts

The Compare feature lets you see how a different prompt, model, or a parameter setting changes the model's output. You can view each of the prompts and their responses side by side to compare and analyze in the following ways:

- With a new prompt.
- With another saved prompt.
- With a ground truth.

## Before you begin

To access the Compare feature, follow these steps:

1. In the Google Cloud console, go to the **Create prompt** page.
	[Go to Create prompt](https://console.cloud.google.com/vertex-ai/studio/multimodal)
2. Select **Compare**. The **Compare** page appears.

## Create a prompt in the Compare feature

On the **Compare** page, you can create a prompt before selecting another prompt to compare results.

To create a prompt, follow these steps:

1. In the **New Prompt** field, enter your prompt.
2. Click **Submit prompts**. The model's response appears below the prompt text that you entered.
3. Click **Save as new**. A **Save prompt** dialog appears.
4. Enter the name of your new prompt in the **Prompt name** field.
5. Select your region in the **Region** field, or leave it as the default region.
6. If a customer-managed encryption key (CMEK) applies, do the following:
	1. Select the **Customer-managed encryption key (CMEK)** checkbox.
	2. Select a key from the **Select a Cloud KMS key** field.
7. Click **Save**, which saves your prompt in the list of prompts to use on the **Compare saved prompt** page.
8. Click **Submit prompts** to compare the prompts and their responses.

You can update your prompts, and save updated versions as new prompts.

## Compare with a new prompt

To compare your saved prompt with a new prompt, follow these steps:

1. Click **Compare new prompt**. A **Compare** pane appears.
2. Optional: Click **Switch model** to use a different model from the default model.
3. Optional: Expand **Outputs**.

##### Outputs:

1. Optional: If you want the model to output in a specific format such as JSON, click the **Structured output** toggle. After you select **Structured output**, the Grounding options are turned off, because grounding isn't supported with structured output.
2. Optional: Change the **Thinking budget** to one of the following options:
- **Auto**: The model only thinks when it needs to. The model adjusts how much it thinks or analyzes a situation based on what's needed at the time.
	- **Manual**: You can adjust the thinking budget tokens.
	- **Off**: No thinking or budgets are used.
1. Optional: Expand **Tools**.

##### Tools:

1. Select one of the following options:
- **Grounding: Google**: Grounding with Google Search or Google Maps.
	- **Grounding: Your data**: Grounding with Vertex AI RAG Engine, Vertex AI Search or Elasticsearch.
1. If you select **Grounding: Your data**, select the data source that you want to use.
2. Optional: Expand **Advanced**:

##### Advanced:

1. Select **Region**.
2. Select **Safety Filter Settings**. A dialog appears. Keep the default of **Off**, or you can specify **Block few**, **Block some**, or **Block most** for each of the following options:
- **Hate speech**: Negative or harmful comments targeting identity or protected attributes.
	- **Dangerous content**: Promotes or enables access to harmful goods, services, and activities.
	- **Sexually explicit content**: Contains references to sexual acts or other lewd content.
	- **Harassment content**: Malicious, intimidating, bullying, or abusive comments targeting another individual.
4. Click **Save** to save the settings and close the dialog.
5. Select the temperature from the **Temperature** field. The temperature controls the randomness in token selection. A lower temperature is good when you expect a true or correct response. A higher temperature can lead to diverse or unexpected results.
6. Select the output token limit from the **Output token limit** field. Output token limit determines the maximum amount of text output from one prompt. A token is approximately four characters.
7. Select the maximum responses from the **Max responses** field. If the maximum number of model responses generated per prompt. Because of safety filters or other policies, responses can still be blocked.
8. Select a value from the **Top-P** field. The Top-p changes how the model selects tokens for output.
9. Click toggle on the **Stream model responses** field. If selected, the responses are printed as they're generated.
10. Enter a stop sequence in the **Add stop sequence** field. Press **Enter** after each sequence.
11. Click **Save** to save changes to your settings.
12. Click **Apply**.
13. Click **Submit prompts** to compare the prompts and their responses.

For more information on token limits for each model, see [Control the thinking budget](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/thinking#budget).

## Compare with another saved prompt

To compare your saved prompt with another saved prompt, follow these steps:

1. Click **Compare saved prompt**. The **Existing Prompt** pane appears.
2. Choose up to two existing prompts to compare.
	1. Select a **Prompt name**. If you have many prompts in your list, click in the **Filter** field, and select the property that you want to filter by. Enter a value, and press Enter.
	2. Click **Apply**. The **Compare** page displays the prompt that you've selected alongside other prompts that you've created or selected for comparison.
3. Click **Submit prompts** to compare the prompts and their responses.

## Compare with a ground truth

Ground truth is your preferred answer to the prompt. All other model responses are evaluated against the ground truth answer.

To compare your saved prompt with a ground truth, follow these steps:

1. Click **Ground truth**. The **Ground truth** pane appears.
2. Enter your ground truth to generate additional evaluation metrics.
3. Click **Save** to save the ground truth.
4. Click **Submit prompts** to compare the prompts and their responses.

The evaluation metrics that are generated when you compare a prompt with a ground truth aren't affected by the region that you select.

# Instruct the model to explain its reasoning

When you tell the model to explain its reasoning, the model responds with the steps that it employs to solve the problem. Going through this process can sometimes improve accuracy and nuance, especially for challenging queries.

The reasoning steps are included as part of the response. To parse out the reasoning steps from the answer that you're looking for, you can specify an output format by using XML or other separators.

## Examples

For example, suppose you're writing a cooking blog and you want the model to tell you how readers might interpret different parts of the blog. If you don't instruct the model to explain its reasoning, the response from the model might not be as useful as you'd like:

| No reasoning |
| --- |
| ``` What is the most likely interpretation of this sentence?          The sentence: "The chef seasoned the chicken and put it in the oven because it looked pale." ``` ``` The chef seasoned the chicken and put it in the oven because it lacked color and needed cooking. ``` |

While you learned about how the model predicts readers might interpret the sentence, it might be useful for you to understand more about the specific predictions that the model made to produce the response. As demonstrated in the following example, the quality of the response might also improve:

| Explain reasoning |
| --- |
| ``` What is the most likely interpretation of this sentence? Explain your reasoning          The sentence: "The chef seasoned the chicken and put it in the oven because it looked pale." ``` ``` Interpreting "The chef seasoned the chicken and put it in the oven because it looked pale."        The most likely interpretation is that the chef seasoned the chicken to add flavor and color, then put it in the oven to cook it.        Here's the reasoning:        - Seasoning is typically used to enhance the flavor of food. Chefs often use spices, herbs, and other ingredients to make their dishes more appealing.       - "Pale" suggests the chicken lacked visual appeal before being seasoned. This could imply it was unseasoned or simply lacking color from spices.       - Putting the chicken in the oven is a common cooking method. The sentence implies the chef's intention is to cook the chicken, not just season it.        Therefore, the chef's actions are likely aimed at both improving the taste and appearance of the chicken through seasoning and then cooking it in the oven. ``` |

Another technique you can use to improve the model's response is to instruct the model to think step-by-step and explain it's reasoning. This requires the model to break down the input into steps and provide the reasoning its using to solve the problem:

| Think step-by-step |
| --- |
| ``` What is the most likely interpretation of this sentence? Think step by step and print out     the thinking process.      Please output in JSON format with final answer in 'answer', and thinking steps in 'think' fields.          The sentence: "The chef seasoned the chicken and put it in the oven because it looked pale." ``` ```json {       "answer": "The chef seasoned the chicken to enhance its flavor and put it in the oven to cook it because it appeared to be undercooked.",       "think": [         {           "step": 1,           "thought": "The chef seasoned the chicken. This suggests that the chef is preparing the chicken for cooking."         },         {           "step": 2,           "thought": "The chef put the chicken in the oven. This indicates that the chef is cooking the chicken."         },         {           "step": 3,           "thought": "The sentence states that the chicken looked pale. Pale chicken is often undercooked."         },         {           "step": 4,           "thought": "Combining these observations, it is most likely that the chef seasoned the chicken to enhance its flavor and put it in the oven to cook it because it appeared to be undercooked."         }       ]     } ``` |

By prompting the model to print out its thinking process, the model generated a more thorough response and you learned more about how it generated that response.

# Break down complex tasks into simpler prompts

For complex tasks that require multiple instructions or steps, you can improve the model's responses by breaking your prompts into subtasks. Smaller prompts can help you improve controllability, debugging, and accuracy.

There are two ways to break down complex prompts and ingest them into a model:

- **Chain prompts:** split a task into subtasks and run the subtaks sequentially.
- **Aggregate responses:** split a task into subtasks and run the subtasks in parallel.

## Chain prompts

For complex tasks that involve multiple *sequential* steps, make each step a prompt and chain the prompts together in a sequence. In this sequential chain of prompts, the output of one prompt in the sequence becomes the input of the next prompt. The output of the last prompt in the sequence is the final output.

### Example

For example, suppose you run a telecommunications business and want to use a model to help you analyze customer feedback to identify common customer issues, classify issues into categories, and generate solutions for categories of issues.

#### Task 1: identify customer issues

The first task you want the model to complete is extracting meaningful data from raw customer feedback. A prompt that achieves this task might be similar to the following, where `CUSTOMER_FEEDBACK` is a file that contains the customer feedback:

| Extract data |
| --- |
| ``` Extract the main issues and sentiments from the customer feedback on our telecom services.       Focus on comments related to service disruptions, billing issues, and customer support interactions.       Please format the output into a list with each issue/sentiment in a sentence, separated by semicolon.        Input: CUSTOMER_FEEDBACK ``` |

We would expect the model's response to contain a list of extracted issues and sentiment from the customer feedback.

#### Task 2: classify issues into categories

Next, you want to prompt the model to classify the data into categories so that you can understand the types of issues customers face, using the response from the previous task. A prompt that achieves this task might look similar to the following, where `TASK_1_RESPONSE` is the response from the previous task:

| Classify data |
| --- |
| ``` Classify the extracted issues into categories such as service reliability, pricing concerns, customer support quality, and others.         Please organize the output into JSON format with each issue as the key, and category as the value.          Input: TASK_1_RESPONSE ``` |

We would expect the model's response to contain categorized issues.

#### Task 3: generate solutions

Now, you want to prompt the model to generate actionable recommendations based on the categorized issues to improve customer satisfaction, using the response from the previous task. A prompt that achieves this might look similar to the following, where `TASK_2_RESPONSE` is the response from the previous task:

| Generate suggestions |
| --- |
| ``` Generate detailed recommendations for each category of issues identified from the feedback.         Suggest specific actions to address service reliability, improving customer support, and adjusting pricing models, if necessary.         Please organize the output into a JSON format with each category as the key, and recommendation as the value.          Input: TASK_2_RESPONSE ``` |

We would expect the model's response to contain recommendations for each category, aimed at improving customer experience and service quality, which satifies our overall objective.

## Aggregate responses

In cases where you have complex tasks but you don't need to perform the tasks in a specific order, you can run parallel prompts and aggregate the model's responses.

### Example

For example, suppose you own a record store and want to use a model to help you decide which records to stock based on music streaming trends and your store's sales data.

#### Task 1: analyze data

The first thing you need to do is analyze the two datasets, streaming data and sales data. You can run the prompts to complete these tasks in parallel. Prompts that achieve these tasks might be similar to the following, where `STORE_SALES_DATA` is a file that contains the sales data and `STREAMING_DATA` is a file that contains the streaming data:

| Task 1a: analyze sales data |
| --- |
| ``` Analyze the sales data to identify the number of sales of each record.       Please organize the output into a JSON format with each record as the key, and sales as the value.        Input: STORE_SALES_DATA ``` |

We would expect the output to contain the number of sales for each record, formatted in JSON.

| Task 1b: analyze streaming data |
| --- |
| ``` Analyze the streaming data to provide a the number of streams for each album.         Please organize the output into a JSON format with each album as the key, and streams as the value.          Input: STREAMING_DATA ``` |

We would expect the output to contain the number of streams for each album, formatted in JSON.

#### Task 2: aggregate data

Now you can aggregate the data from both datasets to help you plan your purchasing decisions. To aggregate the data, include the output from both tasks as the input. A prompt that achieves this might look similar to the following, where `TASK_1A_RESPONSE` and `TASK_1B_RESPONSE` are the responses from the previous tasks:

| Aggregate sales and streaming data |
| --- |
| ``` Recommend a stocklist of about 20 records based on the most sold and most streamed records.         Roughly three quarters of the stock list should be based on record sales, and the rest on streaming.        Input: TASK_1A_RESPONSE and TASK_1B_RESPONSE ``` |

We would expect the output to contain a suggested stocklist of about 20 records, based on record sales and streams, with more favor given to records with proven sales history than to those with more streaming popularity.

# Experiment with parameter values

Each call that you send to a model includes parameter values that control how the model generates a response. The model can generate different results for different parameter values. Experiment with different parameter values to get the best values for the task. The parameters available for different models may differ. The most common parameters are the following:

- Max output tokens
- Temperature
- Top-P
- Top-K
- Seed

## Max output tokens

Maximum number of tokens that can be generated in the response. A token is approximately four characters. 100 tokens correspond to roughly 60-80 words.

Specify a lower value for shorter responses and a higher value for potentially longer responses.

## Temperature

The temperature is used for sampling during response generation, which occurs when `topP` and `topK` are applied. Temperature controls the degree of randomness in token selection. Lower temperatures are good for prompts that require a less open-ended or creative response, while higher temperatures can lead to more diverse or creative results. A temperature of `0` means that the highest probability tokens are always selected. In this case, responses for a given prompt are mostly deterministic, but a small amount of variation is still possible.

If the model returns a response that's too generic, too short, or the model gives a fallback response, try increasing the temperature. If the model enters infinite generation, increasing the temperature to at least `0.1` may lead to improved results.

`1.0` is the recommended starting value for temperature.

Gemini models support a temperature value between 0.0 and 2.0. Models have a default temperature of 1.0.

## Top-P

Top-P changes how the model selects tokens for output. Tokens are selected from the most probable to least probable until the sum of their probabilities equals the top-P value. For example, if tokens A, B, and C have a probability of 0.3, 0.2, and 0.1 and the top-P value is `0.5`, then the model will select either A or B as the next token by using temperature and excludes C as a candidate.

Specify a lower value for less random responses and a higher value for more random responses.

## Top-K

Top-K changes how the model selects tokens for output. A top-K of `1` means the next selected token is the most probable among all tokens in the model's vocabulary (also called greedy decoding), while a top-K of `3` means that the next token is selected from among the three most probable tokens by using temperature.

For each token selection step, the top-K tokens with the highest probabilities are sampled. Then tokens are further filtered based on top-P with the final token selected using temperature sampling.

Specify a lower value for less random responses and a higher value for more random responses.

## Seed

When seed is fixed to a specific value, the model makes a best effort to provide the same response for repeated requests. Deterministic output isn't guaranteed. Also, changing the model or parameter settings, such as the temperature, can cause variations in the response even when you use the same seed value. By default, a random seed value is used.

This is a preview feature.

# Prompt iteration strategies

Prompt design often requires a few iterations before you get the desired response consistently. Your prompt design strategy should apply the [Prompt design best practices](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/prompt-design-strategies#best-practices), with incremental refinements. You can iteratively introduce some or all of the best practices when testing for performance that meets your use case needs.

Additionally, the order of the content in the prompt can sometimes affect the response. Try changing the content order and see how the response changes. For example, for multimodal prompts, try adding the files to the prompt before the instructions.

As you receive responses from the model, take note of the aspects that you like and dislike about its responses and modify your prompts to guide the model to responses that best align with your use cases.

## Examples

In this example, let's say you want the model to write ad copy for your product. You could start by defining the following prompt content:

- **Objective:** Create ad copy
- **Context:**
	- Categories: scarcity, exclusivity
	- Product description: "Chromecast is a device that allows users to wirelessly cast their content from other devices, so they can watch their favorite movies, TV shows, photos, websites, and more on their TV. Chromecast can display content from Android smartphones and tablets, iPhones & iPads, Windows and Mac laptops, and the Chromebook Pixel."
- **Constraints:** Each response should be two sentences or less.

Experimenting with how you provide the content to the model can help you to ensure that the model's response best fits your needs. Suppose you give the model the prompt content exactly as written:

| First iteration |
| --- |
| ``` Create ad copy.        Categories: scarcity, exclusivity        Product description: "Chromecast is a device that allows users to wirelessly cast their content from other devices, so they can watch their favorite movies, TV shows, photos, websites, and more on their TV. Chromecast can display content from Android smartphones and tablets, iPhones & iPads, Windows and Mac laptops, and the Chromebook Pixel."        Constraints: Each response should be two sentences or less. ``` ``` Scarcity        *  Time is running out to experience the future of entertainment! Get your Chromecast before they're gone.       *  Limited quantities available! Don't miss your chance to own the streaming device everyone's talking about.        Exclusivity        *  Unlock a world of entertainment with Chromecast. Experience the freedom of streaming like never before.       *  Upgrade your home entertainment with the exclusive Chromecast device. Join the elite group of cord-cutters who stream smarter. ``` |

Then you can try reformatting the prompt to see how the response changes when the prompt objective, constraints, and some of the context are combined into a single sentence:

| Second iteration |
| --- |
| ``` Create scarcity and exclusivity-focused ad copy that is less than two sentences.        Product description: "Chromecast is a device that allows users to wirelessly cast their content from other devices, so they can watch their favorite movies, TV shows, photos, websites, and more on their TV. Chromecast can display content from Android smartphones and tablets, iPhones & iPads, Windows and Mac laptops, and the Chromebook Pixel." ``` ``` Options for Scarcity & Exclusivity-Driven Chromecast Ads:        Option 1 (Scarcity): "Limited quantities available! Get your Chromecast today before they're gone and unlock a world of on-demand entertainment."        Option 2 (Exclusivity): "Experience entertainment like never before. Chromecast: the ultimate upgrade for your TV, available for a limited time." ``` |

This time, the model's response contained only one copy option for each category. If you realize that you need at least two options for each category and that you don't want to limit the length of the response, you can modify the constraints and try your prompt again:

| Third iteration |
| --- |
| ``` Create two ad-copies about scarcity and two ad-copies about exclusivity.        Product description: "Chromecast is a device that allows users to wirelessly cast their content from other devices, so they can watch their favorite movies, TV shows, photos, websites, and more on their TV. Chromecast can display content from Android smartphones and tablets, iPhones & iPads, Windows and Mac laptops, and the Chromebook Pixel." ``` ``` Scarcity Ad Copies:     Ad 1:      Headline: Don't miss out! Chromecast is flying off the shelves!      Body: Experience the magic of Chromecast before it's too late! Limited quantities are available, so grab yours now and start enjoying your favorite entertainment on the big screen.       Ad 2:      Headline: Last chance! Chromecast is almost sold out.      Body: Time is running out to get your hands on Chromecast. Upgrade your TV experience today and enjoy seamless streaming from all your devices. Don't wait, supplies are limited!      Exclusivity Ad Copies:      Ad 1:      Headline: Unlock a world of entertainment with the exclusive Chromecast.      Body: Join the elite group of Chromecast users and experience the future of television. Enjoy effortless streaming, endless entertainment options, and unparalleled convenience. Chromecast: It's not just TV, it's an experience.      Ad 2:      Headline: Elevate your home entertainment with the Chromecast advantage.      Body: Go beyond ordinary TV with Chromecast. Seamlessly stream content from all your devices and enjoy a personalized entertainment experience like no other. Discover the exclusivity of Chromecast today. ``` |

In the third iteration, the model's response contained both headline and body fields for the ad copy. For this example, let's say that this response aligns with your ad copy requirements.

Now that you've adjusted the prompt to get a response that aligns with your ad copy requirements, you can update and test the prompt to ensure the model produces similarly formatted responses in the future:

| Fourth iteration |
| --- |
| ``` Create two ad-copies about scarcity and two ad-copies about exclusivity.        Include a headline and body for each ad copy.        Product description: "Chromecast is a device that allows users to wirelessly cast their content from other devices, so they can watch their favorite movies, TV shows, photos, websites, and more on their TV. Chromecast can display content from Android smartphones and tablets, iPhones & iPads, Windows and Mac laptops, and the Chromebook Pixel." ``` ``` Scarcity Ads:      Ad 1:      Headline: Last Chance! Chromecast is Selling Out Fast     Body: Get the Chromecast experience before it's gone! Limited quantities remain. Upgrade your TV time today!      Ad 2:      Headline: Don't Miss Out! Chromecast Stock is Running Low     Body: Time is running out to grab your Chromecast. Enjoy seamless streaming on the big screen. Order now while supplies last!      Exclusivity Ads:      Ad 1:      Headline: Unlock the Ultimate Viewing Experience with Chromecast     Body: Join the elite group of Chromecast users and enjoy unparalleled streaming convenience. Elevate your entertainment today!      Ad 2:      Headline: Experience the Future of Entertainment: Get Your Chromecast     Body: Be among the first to enjoy the cutting-edge technology of Chromecast. Stream anything, anytime, effortlessly.  Upgrade your home entertainment now! ``` |

This time, the model's response is very similar to the previous iteration, even with the additional constraints, which means that you successfully iterated upon your prompt.

As demonstrated by the example, prompt iteration is an integral part of the prompt design process that can be used to help you guide the model to produce the best results for your use case.