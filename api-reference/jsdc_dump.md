# jsdc_dump

The `jsdc_dump` function is used to dump a dataclass object to a JSON configuration file.

## Signature

```python
def jsdc_dump(config: T, file_path: str) -> None:
    ...
```

## Parameters

- `config` (T): The dataclass object to be dumped to JSON.
- `file_path` (str): The path where the JSON configuration file should be written.

## Return Value

This function does not return a value. It writes the JSON data to the specified file.

## Important Notes About Fields

### Handling Complex Types

When dumping dataclasses with complex types (nested dataclasses, enums, etc.), ensure they were properly initialized using `field(default_factory=lambda: ...)`:

```python
from dataclasses import dataclass, field
from enum import Enum

class LogLevel(Enum):
    DEBUG = "debug"
    INFO = "info"
    ERROR = "error"

@dataclass
class LoggerConfig:
    # Enum type using default_factory
    level: LogLevel = field(default_factory=lambda: LogLevel.INFO)

@dataclass
class AppConfig:
    # Nested dataclass using default_factory
    logger: LoggerConfig = field(default_factory=lambda: LoggerConfig())
    app_name: str = "MyApp"

# Create and dump configuration
config = AppConfig()
jsdc_dump(config, 'config.json')
```

### Serialization Behavior

- Enum values are serialized to their string representations
- Nested dataclasses are serialized as nested JSON objects
- Complex types initialized with default_factory are properly handled

## Basic Usage Example

```python
from dataclasses import dataclass
from jsdc_loader import jsdc_dump

@dataclass
class DatabaseConfig:
    host: str = 'localhost'
    port: int = 3306
    user: str = 'root'
    password: str = 'password'

# Create a configuration object
db_config = DatabaseConfig(host='example.com', port=5432)

# Dump configuration to 'config.json'
jsdc_dump(db_config, 'config.json')
```

## Additional Notes

- The function will automatically convert Python data types to the appropriate JSON types.
- If a file already exists at the specified path, it will be overwritten.
- The resulting JSON file will be formatted with indentation for readability.
- For complex types (nested dataclasses, enums), the function expects them to be initialized using `field(default_factory=lambda: ...)`.
