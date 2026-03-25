# Foundations of AI in Backend Systems

---

## 1. What LLMs are (Transformers, Tokens)

### Core Concepts
- What is a Large Language Model (LLM)  
- Pretraining vs fine-tuning  
- Autoregressive text generation  
- Probability distributions over tokens  

### Transformer Architecture (High-Level)
- Attention mechanism (self-attention)  
- Why transformers replaced RNNs/LSTMs  
- Input embeddings  
- Positional encoding  
- Encoder vs decoder models  

### Tokens (VERY Important in Practice)
- What is a token (not equal to word!)  
- Tokenization strategies (BPE, WordPiece)  
- Token limits per model  
- Token counting strategies  
- Token overflow handling  

### Practical Backend Implications
- Why long prompts fail  
- Why summarization is needed  
- Cost tied to tokens  

---

## 3. Prompt vs Completion Models

### Model Types
- Completion models (legacy style)  
- Chat models (role-based messages)  
- Instruction-tuned models  

### Prompt Structure
- System message vs user message vs assistant  
- Instruction vs context vs examples  

### Use Cases
- When to use completion-style  
- When to use chat-based APIs (like OpenAI API)  

### Backend Design Implications
- Stateless vs stateful conversations  
- Prompt templating strategies  
- Reusability of prompts  

---

## 5. Determinism vs Randomness (Temperature)

### Parameters Controlling Output
- Temperature (0 → deterministic, 1+ → creative)  
- Top-p (nucleus sampling)  
- Frequency penalty  
- Presence penalty  

### Behavior Tuning
- Deterministic outputs for:
  - Code generation  
  - Data extraction  
- Creative outputs for:
  - Content generation  
  - Brainstorming  

### Backend Implications
- Reproducibility issues  
- Testing challenges  
- Consistency vs diversity tradeoff  

---

## 7. Tokens, Context Windows, Cost Models

### Context Window
- What it is (max tokens per request)  
- Input tokens vs output tokens  
- Sliding window strategies  

### Cost Model
- Cost per 1K tokens  
- Input vs output pricing differences  
- Cost estimation strategies  

### Optimization Techniques
- Prompt compression  
- Summarization pipelines  
- Chunking large documents  
- Caching responses  

### Backend Design Implications
- Budget-aware systems  
- Cost monitoring per request  
- Multi-tier model usage (cheap vs expensive)  

---

## 9. Latency vs Accuracy Tradeoffs

### Latency Sources
- API call time  
- Model size impact  
- Network overhead  

### Accuracy Factors
- Model quality  
- Prompt quality  
- Context size  

### Tradeoffs
- Smaller model → faster, less accurate  
- Larger model → slower, more accurate  

### Backend Strategies
- Async processing  
- Streaming responses  
- Caching frequent queries  
- Fallback models  

---

## 11. AI vs Traditional Microservices

### Traditional Systems
- Deterministic logic  
- Rule-based decisions  
- Exact outputs  

### AI Systems
- Probabilistic outputs  
- Non-deterministic behavior  
- Approximate answers  

### Key Differences
- Testing strategies  
- Debugging complexity  
- Observability needs  

### Hybrid Architectures
- AI + rules engine  
- AI as decision support, not authority  

---

## 13. AI System Architecture Patterns

### Common Patterns
- LLM as a service  
- Backend-for-frontend (AI gateway)  
- AI microservice  
- Event-driven AI processing  

### RAG Architecture
- Retriever + generator pattern  
- Data pipelines for embeddings  

### Agent-Based Systems
- Planner + executor  
- Tool-using agents  

### Integration Patterns
- REST APIs  
- Messaging queues  
- Batch processing  

---

## 15. When NOT to Use AI (Critical for Senior Roles)

### Bad Use Cases
- Deterministic calculations  
- Simple CRUD logic  
- High-precision requirements (e.g. finance transactions)  
- Real-time ultra-low latency systems  

### Risks
- Hallucinations  
- Unreliable outputs  
- Cost explosion  
- Security issues  

### Decision Framework
Ask:  
- Can this be solved with rules?  
- Is approximation acceptable?  
- Is explainability required?  

### Smart Usage Pattern
**AI for:**  
- Interpretation  
- Summarization  
- Decision support  

**NOT for:**  
- Core business invariants
