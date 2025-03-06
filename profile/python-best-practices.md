# Best Practices for Python Development

## Table of Contents
1. [Introduction](#introduction)
2. [Code Structure](#code-structure)
3. [Naming Conventions](#naming-conventions)
4. [Memory Management](#memory-management)
5. [Data Types and Structures](#data-types-and-structures)
6. [Functions and Methods](#functions-and-methods)
7. [Classes](#classes)
8. [Commenting and Documentation](#commenting-and-documentation)
9. [Error Handling](#error-handling)
10. [Portability](#portability)
11. [Performance Optimization](#performance-optimization)
12. [Dependencies Management](#dependencies-management)
13. [Testing](#testing)
14. [Version Control](#version-control)
15. [Code Quality Tools](#code-quality-tools)
16. [Contributing Guidelines](#contributing-guidelines)

## Introduction

This document outlines best practices for Python development in our project. These guidelines aim to ensure code quality, maintainability, and reliability while leveraging Python's strengths: readability, flexibility, and extensive ecosystem.

## Code Structure

### Project Organization

- Use a clear and consistent directory structure:
  ```
  /project-root
    /project_name       # Main package
      /__init__.py      # Package initializer
      /core/            # Core functionality
      /utils/           # Utility functions
      /models/          # Data models
      /api/             # API endpoints
    /tests              # Test code
    /docs               # Documentation
    /scripts            # Standalone scripts
    /examples           # Example usage
    README.md           # Project overview
    requirements.txt    # Dependencies
    setup.py            # Package setup
    .gitignore          # Git ignore file
    pyproject.toml      # Modern project configuration
  ```

### Module Organization

- Follow the "one responsibility per module" principle
- Keep modules focused and cohesive
- Limit file size (suggested maximum ~500 lines)
- Use consistent file naming: `lowercase_with_underscores.py`
- Import organization:
  ```python
  # Standard library imports
  import os
  import sys
  from datetime import datetime
  
  # Third-party imports
  import numpy as np
  import pandas as pd
  
  # Local application imports
  from project_name.utils import helper
  from project_name.models import user
  ```

## Naming Conventions

- Follow PEP 8 naming conventions:
  - `lowercase_with_underscores` for variables, functions, methods, modules, and packages
  - `CapitalizedWords` (PascalCase) for classes
  - `UPPERCASE_WITH_UNDERSCORES` for constants
  - `_leading_underscore` for private attributes/methods
  - `__double_leading_underscore` for name mangling in classes

```python
# Constants
MAX_BUFFER_SIZE = 128
DEFAULT_TIMEOUT = 30

# Classes
class UserProfile:
    pass

# Functions
def calculate_average(values):
    pass

# Variables
user_count = 0
active_connections = []

# Private methods/variables
def _internal_helper():
    pass
```

## Memory Management

- Be mindful of memory usage for large data structures
- Use generators for large data processing:
  ```python
  # Instead of
  def get_all_lines(file):
      return [line for line in file]
  
  # Prefer
  def get_all_lines(file):
      for line in file:
          yield line
  ```
- Use context managers for resource cleanup:
  ```python
  with open('file.txt', 'r') as f:
      data = f.read()
  # File is automatically closed
  ```
- Be aware of mutable default arguments:
  ```python
  # Problematic
  def append_to(element, to=[]):
      to.append(element)
      return to
  
  # Better
  def append_to(element, to=None):
      if to is None:
          to = []
      to.append(element)
      return to
  ```
- Use object pools or caching for expensive objects
- Profile memory usage for critical applications

## Data Types and Structures

- Use appropriate data structures for your use case:
  - Lists for ordered, mutable sequences
  - Tuples for immutable sequences
  - Sets for unique, unordered elements
  - Dictionaries for key-value mappings
  - Named tuples for lightweight immutable objects
  - Dataclasses for data containers (Python 3.7+)

- Use type hints (Python 3.5+):
  ```python
  def process_items(items: list[str]) -> dict[str, int]:
      result = {}
      for item in items:
          result[item] = len(item)
      return result
  ```

- Consider using enums for related constants:
  ```python
  from enum import Enum, auto
  
  class Status(Enum):
      IDLE = auto()
      RUNNING = auto()
      PAUSED = auto()
      ERROR = auto()
  ```

- Leverage Python's built-in data handling features:
  - List/dictionary comprehensions
  - Unpacking
  - Slicing
  - `collections` module specialized containers

## Functions and Methods

- Follow the single responsibility principle
- Keep functions short and focused (suggested maximum ~50 lines)
- Use descriptive parameter names
- Provide default values for optional parameters
- Use keyword arguments for clarity in function calls
- Document parameters and return values
- Use docstrings for function documentation
- Validate function inputs

```python
def get_user_by_id(user_id: int, include_inactive: bool = False) -> dict:
    """
    Retrieve user information by user ID.
    
    Args:
        user_id: The unique identifier for the user
        include_inactive: Whether to include inactive users
        
    Returns:
        User information as a dictionary
        
    Raises:
        ValueError: If user_id is negative
        UserNotFoundError: If user doesn't exist
    """
    if user_id < 0:
        raise ValueError("User ID cannot be negative")
        
    # Function implementation
    return user_data
```

## Classes

- Use classes to encapsulate related data and behavior
- Follow the single responsibility principle
- Implement magic methods (`__init__`, `__str__`, etc.) as needed
- Use properties for computed attributes:
  ```python
  class Circle:
      def __init__(self, radius):
          self._radius = radius
          
      @property
      def radius(self):
          return self._radius
          
      @radius.setter
      def radius(self, value):
          if value < 0:
              raise ValueError("Radius cannot be negative")
          self._radius = value
          
      @property
      def area(self):
          return 3.14159 * self._radius ** 2
  ```
- Use class methods and static methods appropriately
- Consider dataclasses for data containers (Python 3.7+):
  ```python
  from dataclasses import dataclass
  
  @dataclass
  class Point:
      x: float
      y: float
      
      def distance_from_origin(self) -> float:
          return (self.x ** 2 + self.y ** 2) ** 0.5
  ```
- Use abstract base classes for interfaces:
  ```python
  from abc import ABC, abstractmethod
  
  class DataProcessor(ABC):
      @abstractmethod
      def process(self, data):
          pass
  ```

## Commenting and Documentation

- Write self-documenting code with clear names
- Use docstrings for modules, classes, and functions:
  ```python
  """
  This module provides utilities for data processing.
  
  It includes functions for loading, transforming, and saving data
  in various formats.
  """
  ```

- Follow a consistent docstring style (Google, NumPy, or reStructuredText)
- Document parameters, return values, and exceptions
- Include examples in docstrings for complex functions
- Use comments sparingly for non-obvious implementation details
- Keep comments up-to-date with code changes
- Generate API documentation with tools like Sphinx

## Error Handling

- Use exceptions for error handling:
  ```python
  try:
      result = perform_operation()
  except ValueError as e:
      # Handle value error
  except ConnectionError as e:
      # Handle connection error
  else:
      # Execute if no exceptions
  finally:
      # Always execute
  ```

- Create custom exception classes for your application:
  ```python
  class ApplicationError(Exception):
      """Base exception for the application."""
      pass
      
  class ConfigurationError(ApplicationError):
      """Raised when there is a configuration issue."""
      pass
  ```

- Be specific about caught exceptions
- Provide meaningful error messages
- Log exceptions with appropriate context
- Don't silence exceptions without handling them
- Use contextlib.suppress for intentional exception ignoring:
  ```python
  from contextlib import suppress
  
  with suppress(FileNotFoundError):
      os.remove('file.txt')
  ```

## Portability

- Use pathlib for file path operations (Python 3.4+):
  ```python
  from pathlib import Path
  
  data_dir = Path("data")
  file_path = data_dir / "input.txt"
  
  if file_path.exists():
      with file_path.open('r') as f:
          content = f.read()
  ```

- Be mindful of operating system differences
- Use environment variables for configuration
- Handle encoding issues explicitly:
  ```python
  with open('file.txt', 'r', encoding='utf-8') as f:
      content = f.read()
  ```

- Use cross-platform libraries when possible
- Test on all target platforms

## Performance Optimization

- Write clear, maintainable code first
- Profile before optimizing
- Use appropriate data structures for your use case
- Leverage built-in functions and libraries
- Use generator expressions for large datasets
- Consider numpy for numerical operations
- Use multiprocessing or threading for CPU-bound or I/O-bound tasks:
  ```python
  from concurrent.futures import ProcessPoolExecutor
  
  def process_chunk(chunk):
      # Process data
      return result
  
  with ProcessPoolExecutor() as executor:
      results = list(executor.map(process_chunk, data_chunks))
  ```

- Use PyPy for performance-critical applications
- Document optimization decisions and tradeoffs

## Dependencies Management

- Specify dependencies explicitly in requirements.txt or setup.py
- Use virtual environments for isolation
- Consider using dependency management tools:
  - pip and venv (built-in)
  - Poetry
  - Pipenv
  - conda (for scientific computing)

- Pin dependencies to specific versions for reproducibility:
  ```
  # requirements.txt
  numpy==1.21.0
  pandas==1.3.0
  requests==2.26.0
  ```

- Use semantic versioning for flexibility:
  ```
  # requirements.txt
  numpy>=1.21.0,<2.0.0
  ```

- Document dependency purpose and justification
- Regularly update dependencies for security fixes
- Use .gitignore to exclude virtual environments and cache files

## Testing

- Write tests for all functionality
- Use pytest for testing:
  ```python
  def test_add_function():
      assert add(2, 3) == 5
      assert add(-1, 1) == 0
  ```

- Structure tests to match your module structure
- Write unit tests, integration tests, and end-to-end tests
- Use fixtures for test setup
- Mock external dependencies:
  ```python
  from unittest.mock import patch
  
  @patch('module.requests.get')
  def test_api_call(mock_get):
      mock_get.return_value.status_code = 200
      mock_get.return_value.json.return_value = {'key': 'value'}
      result = call_api()
      assert result == 'value'
  ```

- Use parameterized tests for multiple test cases
- Aim for high test coverage
- Run tests in CI/CD pipeline
- Use TDD (Test-Driven Development) when appropriate

## Version Control

- Use meaningful commit messages
- Follow a branching strategy (e.g., GitFlow, GitHub Flow)
- Use feature branches for new features
- Create pull/merge requests for code review
- Tag releases with version numbers
- Include version information in your package:
  ```python
  # project_name/__init__.py
  __version__ = '1.0.0'
  ```

- Use semantic versioning (MAJOR.MINOR.PATCH)
- Keep a changelog (CHANGELOG.md)
- Consider using pre-commit hooks for code quality checks

## Code Quality Tools

- Use linters to enforce coding standards:
  - Flake8 (combines PyFlakes, pycodestyle, and McCabe complexity)
  - Pylint
  - Black (code formatter)
  - isort (import sorter)

- Configure linters in pyproject.toml or setup.cfg:
  ```toml
  [tool.black]
  line-length = 88
  target-version = ['py38']
  
  [tool.isort]
  profile = "black"
  ```

- Use type checkers:
  - mypy
  - pyright

- Add security scanners:
  - Bandit
  - Safety

- Integrate with CI/CD for automated checks
- Generate code quality reports
- Consider using pre-commit hooks

## Contributing Guidelines

- Follow the coding style in this document
- Submit complete pull requests
- Include tests for new functionality
- Update documentation for changes
- Run linters and tests before submitting code
- Write clear commit messages
- Review others' code constructively
- Use issue tracking for bugs and feature requests
- Keep pull requests focused on a single issue

---

This document is meant to evolve over time. Suggestions for improvements are welcome.
