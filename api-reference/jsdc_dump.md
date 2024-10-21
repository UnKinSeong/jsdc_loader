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

## Usage Example

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

## Notes

- The function will automatically convert Python data types to the appropriate JSON types.
- If a file already exists at the specified path, it will be overwritten.
- The resulting JSON file will be formatted with indentation for readability.
