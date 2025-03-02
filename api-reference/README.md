# API Reference

This section provides detailed information about the API functions provided by JSDC Loader. The library is intentionally kept simple, focusing on two core functions that handle all the necessary operations.

## Core Functions

- [**jsdc_load**](jsdc_load.md): Load JSON configuration files into strongly-typed dataclass objects
- [**jsdc_dump**](jsdc_dump.md): Serialize dataclass objects back to JSON configuration files

## Function Overview

### `jsdc_load(file_path, data_class, encoding='utf-8')`

The `jsdc_load` function reads a JSON file and converts it to a dataclass instance, handling nested structures, enums, and type conversion. [Read more](jsdc_load.md)

```python
from jsdc_loader import jsdc_load
from myapp.config import AppConfig

# Load configuration from file
config = jsdc_load('config.json', AppConfig)
```

### `jsdc_dump(obj, output_path, encoding='utf-8', indent=4)`

The `jsdc_dump` function serializes a dataclass object to a JSON file, properly handling nested dataclasses, enum types, and complex structures. [Read more](jsdc_dump.md)

```python
from jsdc_loader import jsdc_dump
from myapp.config import AppConfig

# Update and save configuration
config = AppConfig()
config.debug = True
jsdc_dump(config, 'config.json')
```

## Type Support

JSDC Loader supports the following types:

- **Simple types**: `str`, `int`, `float`, `bool`
- **Collection types**: `list`, `dict` (with proper type annotations)
- **Complex types**: `Enum`, nested dataclasses
- **Optional types**: `Optional[T]` or `Union[T, None]`

For all complex and collection types, remember to use `field(default_factory=lambda: ...)`.
