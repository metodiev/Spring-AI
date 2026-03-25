# ☕ Spring AI Core Architecture (Deep Dive)

---

## 1. Spring AI Modules Overview

### Core modules
- Chat model integration (LLMs)
- Embedding model integration
- Vector store abstraction
- Prompt templating
- Tool/function calling

### Starter dependencies
- Spring Boot starters for AI
- Auto-configured beans
- Conditional loading based on classpath

### Modular design principles
- Separation of concerns:
  - Model interaction
  - Data retrieval
  - Prompt construction

### Extensibility
- Plug in new model providers
- Replace default implementations
- Custom interceptors

---

## 2. Auto-Configuration (Spring Boot Magic)

### How it works
- Based on `spring.factories` / auto-config classes
- Conditional beans (`@ConditionalOnMissingBean`)
- Environment-driven setup

### What gets auto-configured
- ChatModel beans
- EmbeddingModel beans
- ChatClient
- VectorStore

### Customization
- Override default beans
- Define your own `@Bean`
- Profile-based configuration

### Debugging auto-config
- `--debug` flag in Spring Boot
- Auto-config report
- Bean inspection

---

## 3. ChatClient Lifecycle

### Creation
- Built from a ChatModel
- Usually singleton bean

### Request lifecycle
1. Build prompt  
2. Send to model  
3. Receive response  
4. Map to output  

### Stateful vs stateless usage
- Stateless → each request independent
- Stateful → conversation memory

### Interceptors / hooks
- Pre-processing prompts
- Post-processing responses
- Logging

---

## 4. Model Abstraction Layer

### Why it exists
- Avoid vendor lock-in
- Unified API across providers

### Key abstractions
- ChatModel
- EmbeddingModel
- ImageModel (if used)

### Swappable providers
- OpenAI
- Azure OpenAI
- Local models

### Backend benefits
- Switch models without changing business logic
- Multi-provider fallback strategies

---

## 5. Sync vs Async Calls

### Synchronous calls
- Blocking
- Simple to implement
- Good for:
  - APIs
  - Small workloads

### Asynchronous calls
- Non-blocking
- Better scalability
- Uses:
  - `CompletableFuture`
  - Reactive streams

### When to use what
- Sync → request-response APIs
- Async → batch jobs, pipelines

### Thread management
- Thread pools
- Backpressure handling
- Timeout strategies

---

## 6. Streaming Responses

### What is streaming
- Partial responses returned in chunks
- Token-by-token output

### Benefits
- Lower perceived latency
- Better UX (chat apps)

### Implementation concepts
- Reactive streams (Flux)
- Server-Sent Events (SSE)
- WebSocket integration

### Backend challenges
- Aggregating partial responses
- Handling interruptions
- Timeout + cancellation

---

## 7. Error Handling Patterns

### Common error types
- API errors (rate limits, auth)
- Timeout errors
- Invalid responses
- Token limit exceeded

### Strategies
- Retry with backoff
- Fallback models
- Circuit breakers

### Defensive design
- Validate prompts before sending
- Sanitize outputs
- Handle null/empty responses

### Observability
- Log prompt + response
- Track failures
- Alerting

---

## 8. Configuration via application.yml

### Typical config
```yaml
spring:
  ai:
    openai:
      api-key: YOUR_KEY
      chat:
        model: gpt-4
```
Environment separation
dev / test / prod configs
Secrets management
Dynamic configuration
Feature flags
Runtime switching of models
Best practices
Never hardcode API keys
Use environment variables
Central config management
9. Integration with Spring Boot
Bean lifecycle
Managed by Spring container
Dependency injection
Layered architecture
Controller → Service → AI Client
Integration points
REST controllers
Scheduled jobs
Event listeners
Spring ecosystem synergy
Spring Security → protect AI endpoints
Spring Data → feed data into AI
Spring Cache → cache responses
Hidden Advanced Topics (Senior-Level)
Interceptors / Filters
Modify prompts globally
Add metadata
Inject user context
Multi-model orchestration
Cheap model → filter
Expensive model → final answer
Response post-processing
Convert to structured JSON
Validate schema
Enforce contracts
Common Mistakes
Treating AI calls like normal REST calls
Not handling failures properly
Ignoring cost per request
No observability
Tight coupling to one provider
Mini Project
Spring AI Chat Service

Features:

REST endpoint /ask
Uses ChatClient
Supports:
Sync + Async
Streaming
Logs requests/responses
Configurable model
