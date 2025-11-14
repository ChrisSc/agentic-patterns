# Agentic Patterns Catalog

## Introduction to Agentic Patterns

Agentic patterns are reusable, production-ready architectural blueprints for building AI workflows with observability, efficiency, and quality built in. Rather than building ad-hoc solutions for each AI application, patterns provide proven structures that:

- **Improve Observability**: Built-in logging, token tracking, and cost analysis
- **Enable Optimization**: Per-component tuning (e.g., different models at different steps)
- **Ensure Quality**: Validation gates and consistency checks between steps
- **Accelerate Development**: Start from a tested, documented foundation
- **Support Scaling**: Structured approaches to rate limiting, caching, and resource management

This collection exists to help you build better AI applications faster by learning from and building upon established patterns.

## Pattern Catalog

### Prompt-Chaining: Sequential Task Decomposition

**Category**: Sequential Orchestration
**Location**: [`./templates/prompt-chaining/`](./templates/prompt-chaining/)
**Status**: Production-ready

#### Overview

The prompt-chaining pattern breaks complex tasks into three sequential steps, each with distinct responsibilities:

1. **Analyze**: Parse user intent, extract entities, assess task complexity
2. **Process**: Generate content or insights based on the analysis
3. **Synthesize**: Polish, format, and stream the response to the user

Validation gates between steps ensure quality and allow you to reject low-confidence outputs.

#### When to Use

- **Document Analysis & Summarization**: Extract key insights from long documents
- **Content Generation**: Blog posts, documentation, marketing copy, code comments
- **Data Extraction & Validation**: Structured data from unstructured sources
- **Decision Support**: Comparative analysis, recommendations, evaluations
- **Code Review & Refactoring**: Analyze code, suggest improvements, generate diffs

Use prompt-chaining when your task naturally decomposes into sequential steps where step N depends on the output of step N-1.

#### When NOT to Use

- **Parallel Independent Tasks**: Use the orchestrator-worker pattern instead
- **Simple Single-Turn Requests**: Overhead not justified for trivial tasks
- **Real-Time Bidirectional Conversations**: Not designed for multi-turn chat interactions

#### Key Characteristics

- **Sequential Dependency**: Each step requires output from the previous step
- **Structured Outputs**: Each step produces typed, validatable outputs
- **Quality Gates**: Validation rules between steps ensure confidence thresholds
- **Cost Tracking**: Per-step token counting with USD cost logging
- **Streaming Support**: Responses streamed via Server-Sent Events (SSE)
- **Per-Step Optimization**: Use different Claude models at each step (e.g., Haiku for analysis, Sonnet for processing)
- **Observable**: Structured JSON logging, request tracing, circuit breaker with retry logic

#### Technology Stack

- **Framework**: FastAPI with OpenAI-compatible API
- **Orchestration**: LangGraph StateGraph (v1.0.0+)
- **AI Libraries**: LangChain (v1.0.0+) with langchain-anthropic
- **Models**: Anthropic Claude (Haiku 4.5, Sonnet 4.5)
- **Security**: JWT bearer token authentication, rate limiting, request size validation
- **Validation**: Pydantic v2 with structured outputs
- **Quality**: pytest, black, ruff, mypy, comprehensive test coverage
- **Deployment**: Docker and docker-compose included

#### Configuration Profiles

Start with one of these three profiles and customize for your use case:

| Profile | Models | Cost | Speed | Best For |
|---------|--------|------|-------|----------|
| **Cost-Optimized** | All Haiku | ~$0.006/req | 4-8s | Development, high-volume applications |
| **Balanced** | Haiku (analyze) + Sonnet (process) + Haiku (synthesize) | ~$0.011/req | 5-10s | Production general-purpose use |
| **Accuracy-Optimized** | All Sonnet | ~$0.018/req | 8-15s | Complex tasks, high-stakes decisions |

Each step can be individually configured with different models, temperature, max tokens, and validation rules.

#### Getting Started

1. **Quick Start**: See [`templates/prompt-chaining/README.md`](./templates/prompt-chaining/README.md)
2. **Configuration Guide**: Read [`templates/prompt-chaining/PROMPT-CHAINING.md`](./templates/prompt-chaining/PROMPT-CHAINING.md) for detailed tuning strategies
3. **Architecture Deep Dive**: [`templates/prompt-chaining/ARCHITECTURE.md`](./templates/prompt-chaining/ARCHITECTURE.md) explains the technical implementation
4. **Performance Data**: [`templates/prompt-chaining/BENCHMARKS.md`](./templates/prompt-chaining/BENCHMARKS.md) shows real-world performance metrics
5. **Authentication**: [`templates/prompt-chaining/JWT_AUTHENTICATION.md`](./templates/prompt-chaining/JWT_AUTHENTICATION.md) for securing your API

#### Example Configuration Recipe: Customer Support Automation

Use a cost-optimized configuration with Haiku for quick analysis of support tickets, Sonnet for generating helpful responses, and Haiku for formatting with style guidelines.

#### Example Configuration Recipe: Content Generation

Use a balanced or accuracy-optimized configuration depending on content quality requirements. Per-step configuration allows analyzing source material with Haiku, generating with Sonnet, and synthesizing with Haiku for speed.

#### Next Steps

- Clone or use the template to start building
- Read the pattern guide for configuration strategies
- Check benchmarks for expected performance and costs
- Review example implementations in the template

---

## Future Patterns

### Orchestrator-Worker: Parallel Task Execution

**Category**: Parallel Orchestration
**Status**: Coming soon

For tasks involving parallel independent operationssuch as processing multiple documents simultaneously, running different analyses on the same input, or coordinating multiple specialized agentsthe orchestrator-worker pattern provides a foundation.

**Key differences from prompt-chaining**:
- Parallel execution of independent subtasks
- Task distribution and result aggregation
- Resource pooling and load balancing
- Suitable for batch processing and map-reduce style operations

---

## Pattern Selection Guide

Use this decision tree to choose the right pattern:

### Question 1: Are your steps sequential or parallel?

- **Sequential (each step depends on previous)** ’ Prompt-Chaining
- **Parallel (steps are independent)** ’ Orchestrator-Worker

### Question 2: Key considerations

Once you've identified the right pattern category, consider:

- **Complexity**: How many steps or subtasks?
- **Latency Requirements**: Must responses be streaming? Sub-second?
- **Cost Sensitivity**: Optimize for throughput or accuracy?
- **Observability**: How much logging and tracing do you need?
- **Scalability**: Expected request volume?

### Comparison Matrix

| Feature | Prompt-Chaining | Orchestrator-Worker |
|---------|-----------------|---------------------|
| **Best for** | Sequential, dependent steps | Parallel independent tasks |
| **Execution model** | Linear pipeline | Concurrent workers |
| **State management** | Step-by-step evolution | Distributed state aggregation |
| **Failure handling** | Early exit or retry step | Partial failure tolerance |
| **Cost optimization** | Per-step model selection | Load balancing |
| **Streaming** | Response streaming | Batch or streaming aggregates |

---

## Best Practices Across Patterns

### Configuration Strategy

1. **Start Simple**: Begin with the balanced or cost-optimized profile
2. **Measure**: Track latency, cost, and quality metrics for your use case
3. **Optimize**: Adjust model selection, temperature, and validation rules based on measurements
4. **Document**: Keep notes on what works for your specific problem domain

### Observability & Monitoring

- Enable structured JSON logging in production
- Track token usage and costs across all steps
- Monitor validation gate rejection rates as a quality metric
- Use request IDs for distributed tracing

### Cost Management

- Token usage is logged per stepidentify which steps consume most resources
- Consider model downgrading (e.g., Haiku for analysis phases)
- Batch process when possible to amortize initialization costs
- Monitor cost trends and set up alerts for anomalies

### Testing & Quality

- Each pattern includes a test suiterun it before deploying
- Test with representative real-world inputs
- Validate that quality gates are appropriately tuned
- Use the benchmarking tools provided to establish baselines

### Deployment

- All patterns include Docker containerization
- Use docker-compose for local development, Kubernetes for production
- Environment-based configuration through .env files
- Health check endpoints included

### Documentation

- Each pattern is extensively documentedread the architecture guide
- Keep your configuration choices documented for future maintainers
- Document any custom validation rules or step customizations

---

## Contributing New Patterns

We welcome contributions of new agentic patterns. To propose a pattern:

1. **Start with Documentation**: Describe the pattern, its use cases, and why it's valuable
2. **Provide a Reference Implementation**: A complete, tested, production-ready template
3. **Include Comprehensive Docs**: README, architecture guide, examples, and benchmarks
4. **Demonstrate Value**: Show performance, cost, or capability advantages

See [CONTRIBUTING.md](./CONTRIBUTING.md) for detailed guidelines and submission process.
