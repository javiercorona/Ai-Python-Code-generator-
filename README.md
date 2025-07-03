# AI Coding Assistant - LocalPythonAI

## Overview

LocalPythonAI is an advanced AI-powered coding assistant that runs locally on your machine. It provides code generation, analysis, debugging, and refactoring capabilities for multiple programming languages. Built on top of the DeepSeek Coder model, this tool offers a comprehensive suite of features for developers.

## Features

- **Code Generation**: Generate code from natural language prompts
- **Multi-language Support**: Python, JavaScript, HTML, CSS
- **Code Execution**: Safe execution environment with timeout protection
- **Project Management**: File management and dependency tracking
- **Static Analysis**: Complexity metrics, style checks, security scanning
- **AI-Powered Tools**: Debugging, refactoring, optimization, explanation
- **Documentation**: Auto-generated docstrings in multiple styles
- **Testing**: Test case generation (pytest, unittest, doctest)
- **API Server**: REST interface for integration with other tools
- **Git Integration**: Initialize and manage git repositories

## Installation

### Prerequisites

- Python 3.8+
- pip
- Recommended: NVIDIA GPU with CUDA for faster inference

### Installation Steps

```bash
# Clone the repository
git clone https://github.com/yourusername/localpythonai.git
cd localpythonai

# Create and activate virtual environment (recommended)
python -m venv .venv
source .venv/bin/activate  # Linux/MacOS
.venv\Scripts\activate     # Windows

# Install dependencies
pip install -r requirements.txt

# Install PyTorch with CUDA support (if you have an NVIDIA GPU)
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```

## Usage

### Basic Usage

Start the interactive console:

```bash
python localpythonai.py
```

Example session:

```
>>> Create a Python function to calculate factorial
[AI generates factorial function]
>>> !run
>>> !docs numpy
>>> !tests pytest
>>> !explain
```

### Command Reference

| Command | Description | Example |
|---------|-------------|---------|
| `!help` | Show all commands | `!help` |
| `!run` | Execute last generated code | `!run` |
| `!docs [style]` | Generate documentation | `!docs google` |
| `!tests [framework]` | Generate tests | `!tests unittest` |
| `!profile [detailed]` | Profile code | `!profile detailed` |
| `!explain` | Explain code | `!explain` |
| `!debug [error]` | Debug code | `!debug "IndexError: list index out of range"` |
| `!refactor [goal]` | Refactor code | `!refactor "improve readability"` |
| `!optimize [type]` | Optimize code | `!optimize memory` |
| `!convert <lang>` | Convert code | `!convert javascript` |
| `!language [lang]` | Set language | `!language html` |
| `!git_init [commit]` | Initialize git repo | `!git_init commit` |
| `!save [dir]` | Save project | `!save my_project` |
| `!venv` | Setup virtualenv | `!venv` |
| `!api [port]` | Start API server | `!api 8080` |
| `!exit` | Quit | `!exit` |

### API Usage

Start the API server:

```bash
python localpythonai.py --api
```

Example API requests:

```bash
# Generate code
curl -X POST http://localhost:8000/generate \
  -H "Content-Type: application/json" \
  -d '{"prompt":"Create a Python function to reverse a string"}'

# Execute code
curl -X POST http://localhost:8000/execute \
  -H "Content-Type: application/json" \
  -d '{"code":"print(\"Hello World\")"}'

# Explain code
curl -X POST http://localhost:8000/explain \
  -H "Content-Type: application/json" \
  -d '{"code":"def factorial(n):\n    return 1 if n == 0 else n * factorial(n-1)"}'
```

### Python Module Usage

You can also use LocalPythonAI as a Python module:

```python
from localpythonai import LocalPythonAI

ai = LocalPythonAI(model_name="deepseek-ai/deepseek-coder-1.3b-base")

# Generate code
result = ai.generate("Create a Python function to calculate Fibonacci sequence")
if result["status"] == "success":
    print(result["code"])

# Execute code
exec_result = ai.execute_code("def fib(n):\n    a, b = 0, 1\n    for _ in range(n):\n        a, b = b, a + b\n    return a\nprint(fib(10))")
print(exec_result["output"])
```

## Examples

### 1. Basic Code Generation

```
>>> Create a Python function to check if a number is prime
[AI generates prime checking function]
>>> !run
Enter a number to check: 17
17 is a prime number
```

### 2. Debugging Assistance

```
>>> Create a function that divides two numbers
[AI generates division function]
>>> !run
Enter first number: 10
Enter second number: 0
[Error: Division by zero]
>>> !debug "Division by zero"
[AI provides fixed version with error handling]
```

### 3. Code Conversion

```
>>> Create a Python dictionary with some data
[AI generates Python dictionary]
>>> !convert javascript
[AI converts the dictionary to JavaScript object]
```

### 4. Project Workflow

```
!language python
Create a Flask web application with two routes
!save my_flask_app
!git_init commit
!venv
!tests pytest
```

## Configuration

You can configure the assistant by modifying these parameters when initializing:

```python
ai = LocalPythonAI(
    model_name="deepseek-ai/deepseek-coder-1.3b-base",  # Model to use
    device="cuda",                                      # "cuda" or "cpu"
    max_context_length=8000,                            # Context window size
    max_new_tokens=1024,                                # Max tokens to generate
    temperature=0.7,                                    # Creativity (0-1)
    safety_checks=True,                                 # Enable safety checks
    enable_autocomplete=True,                           # Enable autocomplete
    enable_multilanguage=True                           # Enable multi-language
)
```

## Troubleshooting

1. **CUDA Out of Memory**:
   - Reduce `max_new_tokens`
   - Use smaller model
   - Restart kernel

2. **Slow Performance**:
   - Ensure you're using CUDA if available
   - Reduce `max_context_length`
   - Upgrade hardware

3. **Safety Check Errors**:
   - Disable safety checks (not recommended)
   - Modify prompt to avoid dangerous operations
