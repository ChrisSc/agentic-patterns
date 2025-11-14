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
- Git with support for submodules

### Using a Template

**Option 1: Clone with submodules**
```bash
git clone --recurse-submodules https://github.com/ChrisSc/agentic-patterns.git
cd agentic-patterns/templates/prompt-chaining
```

**Option 2: Use GitHub's template button**
Navigate to the template repository and click "Use this template" to create your own repository.

### Example: Prompt-Chaining Pattern

The prompt-chaining pattern breaks complex tasks into three sequential steps:

```
Analyze → Process → Synthesize
```

Perfect for document summarization, content generation, or data extraction. See the [Prompt-Chaining template](./templates/prompt-chaining/) for a complete working example.

## Available Patterns

### Prompt-Chaining
**Sequential task decomposition with validation gates**

A three-step workflow where each step builds on the previous: analyze user intent, process with the appropriate model, and synthesize a polished response. Includes per-step model configuration, validation gates, and comprehensive cost/performance tracking.

- **Location**: [`./templates/prompt-chaining/`](./templates/prompt-chaining/)
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
└── templates/
    └── prompt-chaining/                # Prompt-chaining pattern (git submodule)
        ├── README.md                   # Pattern quick start
        ├── PROMPT-CHAINING.md          # Detailed pattern guide
        ├── ARCHITECTURE.md             # Technical deep dive
        └── src/                        # Implementation
```

Each template is a complete, standalone repository included as a git submodule.

## Pattern Selection

Not sure which pattern to use? Check [PATTERNS.md](./PATTERNS.md) for a decision framework and comparison guide.

## Contributing

We welcome new agentic patterns that solve real-world problems. Patterns should:
- Be turn-key implementations with comprehensive tests
- Include detailed documentation (README, ARCHITECTURE, examples)
- Demonstrate clear value over ad-hoc implementations
- Follow the quality standards established by existing patterns

See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

## License

This project is licensed under the MIT License. See [LICENSE.md](./LICENSE.md) for details.
