# Usage

This section provides detailed information on how to use JSDC Loader in your Python projects.

JSDC Loader provides two main functions: `jsdc_load` and `jsdc_dump`. Here's how to use them effectively:

## Type Handling Guidelines

### Simple Types

For primitive types (str, int, bool, etc.), you can use direct default values:

```python
from dataclasses import dataclass

@dataclass
class DatabaseConfig:
    host: str = 'localhost'
    port: int = 3306
    user: str = 'root'
    password: str = 'password'
```

### Complex Types

For complex types (Enums, nested dataclasses), you MUST use `field(default_factory=lambda: ...)`:

```python
from dataclasses import dataclass, field
from enum import Enum

class Environment(Enum):
    DEV = "development"
    PROD = "production"

@dataclass
class LoggerConfig:
    # Enum types require default_factory
    env: Environment = field(default_factory=lambda: Environment.DEV)
    level: str = "info"

@dataclass
class AppConfig:
    # Nested dataclasses require default_factory
    logger: LoggerConfig = field(default_factory=lambda: LoggerConfig())
    debug: bool = False
```

## Loading Configuration

To load a JSON configuration file into a dataclass object:

```python
from jsdc_loader import jsdc_load

# Load configuration from 'config.json'
loaded_config = jsdc_load('config.json', AppConfig)

# Access nested configuration
print(loaded_config.logger.env)  # Access enum value
print(loaded_config.debug)       # Access simple value
```

## Dumping Configuration

To dump a dataclass object to a JSON file:

```python
from jsdc_loader import jsdc_dump

# Create configuration with custom values
config = AppConfig()
config.logger.env = Environment.PROD
config.debug = True

# Dump configuration to 'config.json'
jsdc_dump(config, 'config.json')
```

## Best Practices

1. **Type Safety**
   - Always use type hints for all fields
   - Use `field(default_factory=lambda: ...)` for complex types
   - Consider using Enum for fields with fixed choices

```python
@dataclass
class ServerConfig:
    # Good: Using Enum for fixed choices
    mode: ServerMode = field(default_factory=lambda: ServerMode.DEVELOPMENT)
    
    # Good: Using type hints for all fields
    port: int = 8080
    debug: bool = False
```

2. **Nested Configurations**
   - Break down complex configurations into smaller dataclasses
   - Use default_factory for all nested dataclasses

```python
@dataclass
class DatabaseConfig:
    host: str = 'localhost'
    port: int = 3306

@dataclass
class AppConfig:
    # Good: Using default_factory for nested config
    database: DatabaseConfig = field(default_factory=lambda: DatabaseConfig())
    app_name: str = "MyApp"
```

3. **Error Handling**
   - Always validate loaded configurations
   - Provide meaningful defaults for all fields

```python
@dataclass
class Config:
    # Good: All fields have defaults
    timeout: int = 30
    retries: int = 3
    base_url: str = "http://localhost"
```

## Common Pitfalls

1. **Incorrect Complex Type Initialization**
   ```python
   # Bad: Direct assignment of complex types
   config: NestedConfig = NestedConfig()
   
   # Good: Using default_factory
   config: NestedConfig = field(default_factory=lambda: NestedConfig())
   ```

2. **Missing Type Hints**
   ```python
   # Bad: Missing type hint
   name = "default"
   
   # Good: Explicit type hint
   name: str = "default"
   ```

For more detailed examples, check out the [examples](examples/) section.
