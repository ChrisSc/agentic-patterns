# Agentic Patterns

A central collection of turn-key agentic workflow templates for building AI-powered applications with Claude.

## What Are Agentic Patterns?

Agentic patterns are reusable, well-architected blueprints for AI workflows. They provide structured approaches to common AI application problems—like breaking down complex tasks into sequential steps or executing independent operations in parallel—with built-in observability, cost tracking, and quality validation.

## Key Features

- **Turn-Key Templates**: Complete, tested implementations ready to deploy immediately
- **GitHub Repository Templates**: Use the "Use this template" button to create a new repository
- **Comprehensive Documentation**: Each pattern includes architecture guides, configuration strategies, and examples
- **Observable & Measurable**: Token tracking, cost logging, and structured JSON logging included
- **Flexible Configuration**: Per-step model selection, validation gates, rate limiting, and more

## Quick Start

### Prerequisites

- Python 3.10 or higher
- Anthropic API key (for Claude access)
- Git (for cloning repositories)

### Using a Template

**Option 1: Use GitHub's template button**
Navigate to [prompt-chaining](https://github.com/ChrisSc/prompt-chaining) and click "Use this template" to create your own repository.

**Option 2: Clone directly**
```bash
git clone https://github.com/ChrisSc/prompt-chaining.git
cd prompt-chaining
```

### Example: Prompt-Chaining Pattern

The prompt-chaining pattern breaks complex tasks into three sequential steps:

```
Analyze → Process → Synthesize
```

Perfect for document summarization, content generation, or data extraction. See the [Prompt-Chaining template](https://github.com/ChrisSc/prompt-chaining) for a complete working example.

## Available Patterns

### Prompt-Chaining
**Sequential task decomposition with validation gates**

A three-step workflow where each step builds on the previous: analyze user intent, process with the appropriate model, and synthesize a polished response. Includes per-step model configuration, validation gates, and comprehensive cost/performance tracking.

- **When to use**: Document analysis, content generation, data extraction, decision support
- **Key feature**: Validation gates between steps ensure quality
- **Cost**: $0.006–$0.018 per request depending on configuration

For detailed pattern information, see [PATTERNS.md](./PATTERNS.md).

## Repository Structure

```
agentic-patterns/
├── README.md                           # This file
├── PATTERNS.md                         # Pattern catalog and selection guide
├── LICENSE.md                          # MIT License
```

Pattern templates are complete, standalone repositories:
- [Prompt-Chaining](https://github.com/ChrisSc/prompt-chaining)

## Pattern Selection

Not sure which pattern to use? Check [PATTERNS.md](./PATTERNS.md) for a decision framework and comparison guide.

## License

This project is licensed under the MIT License. See [LICENSE.md](./LICENSE.md) for details.
