# Welcome to JSDC Loader

JSDC Loader (JSON Data Class Loader) is a Python utility for loading JSON configuration files into dataclass objects. It provides a simple and type-safe way to manage configuration data in your Python applications by leveraging Python's dataclass and type hinting features.

## Overview

Managing configuration in Python applications can be challenging, especially when dealing with:
- Type safety and validation
- Complex nested structures
- Default values and configuration updates
- Serialization and deserialization

JSDC Loader solves these challenges by providing a clean, type-safe interface between your JSON configuration files and Python code.

## Features

* **Type-Safe Loading**: Convert JSON configuration files into strongly-typed dataclass objects
* **Rich Type Support**: Handle nested dataclasses, Enums, lists, and optional types
* **Validation**: Automatic type checking and conversion for configuration values
* **Default Values**: Proper initialization of complex structures using default_factory
* **Serialization**: Easily dump modified configurations back to JSON with proper formatting

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

## Installation

```bash
pip install jsdc_loader
```

## Quick Example

```python
from dataclasses import dataclass, field
from jsdc_loader import jsdc_load, jsdc_dump

@dataclass
class ServerConfig:
    host: str = "localhost"
    port: int = 8080
    debug: bool = False

# Create default config
config = ServerConfig()

# Save to JSON file
jsdc_dump(config, "server_config.json")

# Later, load from JSON file
loaded_config = jsdc_load("server_config.json", ServerConfig)
print(f"Server running at: {loaded_config.host}:{loaded_config.port}")
```

## Quick Navigation

* [Getting Started](getting-started.md) - Installation and basic setup
* [Usage](usage.md) - Detailed usage information and best practices
* [API Reference](api-reference/) - Complete API documentation
* [Examples](examples/) - Common usage patterns and scenarios 
* [Contributing](contributing.md) - How to contribute to JSDC Loader
* [License](license.md) - License information

## Why JSDC Loader?

JSDC Loader simplifies the process of working with configuration files in Python by leveraging the power of dataclasses and type hinting. It enforces proper initialization patterns for complex types to ensure type safety and prevent common pitfalls in configuration management.

Whether you're working on a small project or a large application, JSDC Loader helps you manage your configuration data more effectively and with fewer errors by enforcing best practices and type safety.

Get started with JSDC Loader today and experience a more streamlined approach to configuration management in Python!
