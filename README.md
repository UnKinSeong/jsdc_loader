# Welcome to JSDC Loader

JSDC Loader (JSON Data Class Loader) is a Python utility for loading JSON configuration files into dataclass objects. It provides a simple and type-safe way to manage configuration data in your Python applications by leveraging Python's dataclass and type hinting features.

## Features

* Load JSON configuration files into dataclass objects
* Support for nested dataclass structures with proper initialization using default_factory
* Type checking and conversion for configuration values
* Support for Enum types and complex nested structures
* Easy updating of configuration from different files
* Ability to dump modified configurations back to JSON

## Key Requirements

When working with complex types (nested dataclasses, enums), JSDC Loader requires the use of `field(default_factory=lambda: ...)` for proper initialization:

```python
from dataclasses import dataclass, field
from enum import Enum

class LogLevel(Enum):
    INFO = "info"
    DEBUG = "debug"

@dataclass
class LoggerConfig:
    # Enum types must use default_factory
    level: LogLevel = field(default_factory=lambda: LogLevel.INFO)

@dataclass
class AppConfig:
    # Nested dataclasses must use default_factory
    logger: LoggerConfig = field(default_factory=lambda: LoggerConfig())
    app_name: str = "MyApp"  # Simple types can use direct defaults
```

## Quick Navigation

* [Getting Started](getting-started.md)
* [Usage](usage.md)
* [API Reference](api-reference/)
* [Examples](examples/)
* [Contributing](contributing.md)
* [License](license.md)

## About

JSDC Loader simplifies the process of working with configuration files in Python by leveraging the power of dataclasses and type hinting. It enforces proper initialization patterns for complex types to ensure type safety and prevent common pitfalls in configuration management.

Whether you're working on a small project or a large application, JSDC Loader helps you manage your configuration data more effectively and with fewer errors by enforcing best practices and type safety.

Get started with JSDC Loader today and experience a more streamlined approach to configuration management in Python!
