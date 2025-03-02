# Getting Started

This guide will help you get started with JSDC Loader, from installation to your first configuration file.

## Installation

To install JSDC Loader, you can use pip:

```bash
pip install jsdc_loader
```

This will install the latest version of JSDC Loader and its dependencies.

You can also update an existing JSDC Loader installation with pip:

```bash
pip install -U jsdc_loader
```

## Requirements

- Python 3.7 or later
- For complex types (nested dataclasses, enums), usage of `field(default_factory=lambda: ...)` is required

## Basic Usage

Here's a simple example to get you started:

```python
from dataclasses import dataclass, field
from enum import Enum
from jsdc_loader import jsdc_load, jsdc_dump

# Simple configuration with primitive types
@dataclass
class DatabaseConfig:
    host: str = 'localhost'
    port: int = 3306
    user: str = 'root'
    password: str = 'password'

# Configuration with complex types
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
    database: DatabaseConfig = field(default_factory=lambda: DatabaseConfig())
    logger: LoggerConfig = field(default_factory=lambda: LoggerConfig())
    app_name: str = "MyApp"  # Simple types can use direct defaults

# Create and save configuration
config = AppConfig()
jsdc_dump(config, 'config.json')

# Load configuration
loaded_config = jsdc_load('config.json', AppConfig)
```

## Understanding the Default Factory Requirement

JSDC Loader requires the use of `field(default_factory=lambda: ...)` for complex types for several important reasons:

1. **Type Safety**: Ensures proper initialization of complex types with their default values
2. **Immutability**: Prevents shared mutable state between instances
3. **Serialization**: Guarantees correct JSON serialization/deserialization

Without using default_factory, you might encounter issues like:
- Shared references between instances
- Improper initialization of nested structures
- Type conversion errors during serialization/deserialization

## Type Handling Guidelines

### Simple Types

For primitive types (str, int, bool, etc.), you can use direct default values:
```python
name: str = "default"
port: int = 8080
```

### Complex Types

For complex types (Enums, nested dataclasses), always use default_factory:
```python
logger: LoggerConfig = field(default_factory=lambda: LoggerConfig())
level: LogLevel = field(default_factory=lambda: LogLevel.INFO)
```

### Collection Types

For collection types (list, dict), also use default_factory:
```python
tags: list[str] = field(default_factory=lambda: ["default"])
properties: dict[str, str] = field(default_factory=lambda: {"key": "value"})
```

### Optional Types

For optional types, use default_factory with None:
```python
username: Optional[str] = field(default_factory=lambda: None)
```

## Next Steps

- Check out the [Usage Guide](usage.md) for more detailed information
- See [Examples](examples/) for more complex usage scenarios
- Review the [API Reference](api-reference/) for detailed documentation
