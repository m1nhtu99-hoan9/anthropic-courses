# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the official Anthropic Courses repository containing educational materials for learning the Claude API and prompt engineering. The repository consists of 5 structured course modules delivered through Jupyter notebooks with supporting Python scripts and evaluation frameworks.

## Course Structure

### 1. Anthropic API Fundamentals (`anthropic_api_fundamentals/`)
- **Purpose**: Core SDK usage, authentication, model parameters, streaming, vision
- **Format**: 6 Jupyter notebooks (`01_getting_started.ipynb` to `06_vision.ipynb`)
- **Key Pattern**: Each notebook builds incrementally on SDK concepts

### 2. Prompt Engineering Interactive Tutorial (`prompt_engineering_interactive_tutorial/`)
- **Purpose**: Comprehensive prompting techniques from basic to advanced
- **Format**: 3 platform variants (Anthropic 1P, AWS Bedrock anthropic/, AWS Bedrock boto3/)
- **Structure**: 9 core chapters + 3 appendix chapters, each with exercises
- **Key Pattern**: Structured progression from basic prompt structure to complex use cases

### 3. Real World Prompting (`real_world_prompting/`)
- **Purpose**: Practical application of prompting techniques in production scenarios
- **Format**: 5 notebooks covering medical, engineering, customer support use cases
- **Key Pattern**: Domain-specific prompt engineering with real-world constraints

### 4. Prompt Evaluations (`prompt_evaluations/`)
- **Purpose**: Production-ready evaluation methodologies and frameworks
- **Format**: 9 lessons progressing from basic to advanced evaluation techniques
- **Key Dependencies**: PromptFoo framework for automated evaluation
- **Key Pattern**: Evaluation complexity increases from manual to automated to model-graded

### 5. Tool Use (`tool_use/`)
- **Purpose**: Claude's function calling capabilities and structured outputs
- **Format**: 6 notebooks from basic tool concepts to multi-tool chatbots
- **Key Pattern**: Progressive complexity from single tools to complete workflows

## Development Environment Setup

### Python Environment
- **Python Version**: 3.12.3 (required: 3.7.1+)
- **Package Manager**: pip not installed in current environment
- **Key Dependencies**: 
  - `anthropic` SDK (0.21.3)
  - `boto3` (1.34.74) for AWS integration
  - `python-dotenv` for environment variables

### Node.js Environment (for PromptFoo evaluations)
- **Node Version**: v24.3.0
- **NPM Version**: 11.4.2
- **PromptFoo**: Not globally installed, needs local installation

### Required Tools Setup
```bash
# Install Python dependencies (from requirements.txt in AmazonBedrock/)
pip install anthropic==0.21.3 boto3==1.34.74 awscli==1.32.74 python-dotenv

# Install Jupyter for running notebooks
pip install jupyter

# For prompt evaluations - install PromptFoo in specific directories
cd prompt_evaluations/05_prompt_foo_code_graded_animals
npm install

# Repeat for other PromptFoo directories (06-09)
```

## Running the Courses

### Jupyter Notebooks
```bash
# Start Jupyter server
jupyter notebook

# Or run specific notebook
jupyter notebook anthropic_api_fundamentals/01_getting_started.ipynb
```

### PromptFoo Evaluations
```bash
# Navigate to evaluation directory
cd prompt_evaluations/05_prompt_foo_code_graded_animals

# Install dependencies
npm install

# Run evaluation
npx promptfoo eval

# View results
npx promptfoo view
```

## Key Architecture Patterns

### Authentication Pattern
All courses use consistent environment variable pattern:
```python
from dotenv import load_dotenv
import os

load_dotenv()
api_key = os.getenv("ANTHROPIC_API_KEY")
```

### Message Format Pattern
Standard Claude API message structure used throughout:
```python
client.messages.create(
    model="claude-3-haiku-20240307",
    max_tokens=1000,
    messages=[{"role": "user", "content": "prompt"}]
)
```

### Evaluation Pattern
PromptFoo configurations follow standard structure:
- `prompts.py`: Contains prompt templates as functions
- `promptfooconfig.yaml`: Defines models, tests, and grading
- `transform.py`: Optional response transformation logic
- `.csv` files: Test datasets

### Exercise Pattern
Each tutorial includes:
- Lesson content explaining concepts
- "Example Playground" for experimentation
- Structured exercises with specific grading criteria
- Hints system (`hints.py`) for guidance

## File Organization Logic

### Notebook Naming Convention
- `00_Tutorial_How-To.ipynb`: Setup and introduction
- `01-09_[Topic].ipynb`: Core lesson sequence
- `10_[N]_Appendix_[Topic].ipynb`: Advanced supplementary material

### Python Script Organization
- `prompts.py`: Prompt template functions (returns formatted strings)
- `transform.py`: Response processing functions
- `hints.py`: Exercise guidance and solutions
- `utils/`: Shared utility functions

### Platform Variants
The prompt engineering tutorial has three identical content variants:
- `Anthropic 1P/`: Direct API usage
- `AmazonBedrock/anthropic/`: AWS Bedrock with Anthropic SDK
- `AmazonBedrock/boto3/`: AWS Bedrock with boto3

## Model Usage Guidelines

### Default Model Selection
- **Primary**: `claude-3-haiku-20240307` (cost-optimized for learning)
- **Comparison**: `claude-3-5-sonnet-20240620` (performance benchmarking)
- **Principle**: Courses favor lowest-cost model for student accessibility

### Model Parameter Patterns
Common parameter combinations used across notebooks:
- `max_tokens`: Typically 1000-2000 for exercises
- `temperature`: Not explicitly set (uses defaults)
- `system`: Used in advanced lessons for role assignment

## Working with This Repository

### Making Changes
- **Notebooks**: Edit directly in Jupyter interface
- **Python Scripts**: Standard text editor workflow
- **Evaluation Configs**: YAML files are hand-edited
- **Test Data**: CSV files for evaluation datasets

### Testing Changes
- **Notebooks**: Run cells sequentially to validate
- **Evaluations**: Use `npx promptfoo eval` to test changes
- **Python Scripts**: Import and test functions directly

### Content Dependencies
- **Sequential Learning**: Each course builds on previous concepts
- **Cross-References**: Lessons reference earlier chapters
- **Shared Utilities**: `hints.py` and `utils/` used across modules