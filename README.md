# spring-ai-zero-to-advanced
Spring AI – Zero to Advanced: Complete Java Learning Guide

1. What are we going to build?
Instead of learning every concept using a different example, let's imagine that we are building one application throughout this guide.

Our example: AI Customer Support Assistant

Imagine an online shopping company. Customers ask questions such as:
- What is your return policy?
- Where is my order?
- Can I return a damaged product?
- How long does delivery take?
- Can you explain your refund policy?
We want to build a Java Spring Boot application that can answer these questions using AI.

As we learn each Spring AI concept, we will understand how it makes this customer-support application smarter.
<img width="768" height="433" alt="image" src="https://github.com/user-attachments/assets/c6e423c9-22a0-4d27-8f68-eb948feecc1b" />

2. What is Spring AI?
Before learning the individual topics, let's understand Spring AI.

Normally, when we develop a Java application, we write business logic ourselves.

For example:

```java
public String getReturnPolicy() {
    return "Products can be returned within 30 days.";
}
```
This works, but the problem is that we need to write separate logic for every possible question.

What if a customer asks:
- Can I send this product back?
- I purchased the wrong item. Can I return it?
- What is the deadline for returning my purchase?
We would need to write logic to handle all these different questions.

This is where AI becomes useful.

Spring AI is a framework that helps Java developers integrate AI models into Spring Boot applications.

It provides a common programming interface to work with different AI providers, such as:
- OpenAI
- Ollama
- Anthropic
- Google Gemini
- Azure OpenAI
Think of Spring AI as a bridge between your Java application and AI models.

<img width="762" height="440" alt="image" src="https://github.com/user-attachments/assets/90d89629-00ee-4b6a-b8d6-4e1a40d1b4e6" />


For example, instead of directly writing HTTP requests to an AI provider, we can use Spring AI's ChatClient.
```java
@RestController
public class CustomerSupportController {

    private final ChatClient chatClient;

    public CustomerSupportController(ChatClient.Builder builder) {
        this.chatClient = builder.build();
    }

    @GetMapping("/support")
    public String askQuestion(@RequestParam String question) {

        return chatClient.prompt()
                .user(question)
                .call()
                .content();
    }
}
```
Let's understand what happens:
1. A customer sends a question.
2. The Spring Boot application receives it.
3. ChatClient sends the question to the configured AI model.
4. The AI model generates an answer.
5. Spring AI returns that answer to our application.
The important thing is that we don't need to manage the low-level API communication ourselves.

PART 1: MULTIPLE LLMs – ONE APPLICATION

3. What are LLMs?
   
LLM stands for Large Language Model.

An LLM is an AI model trained using a large amount of text and other information.

It can understand questions and generate human-like responses.

Examples:
- GPT models from OpenAI.
- Llama models from Meta.
- Gemini models from Google.
- Claude models from Anthropic.
Think of an LLM as an intelligent engine that understands natural language.

For our customer-support application, the LLM is responsible for understanding customer questions and generating answers.
4. OpenAI vs Ollama
Spring AI allows us to connect different LLM providers.

Let's understand two popular choices.
OpenAI










OpenAI

OpenAI provides cloud-based AI models. Our Java application sends requests over the internet to OpenAI and receives generated responses.
