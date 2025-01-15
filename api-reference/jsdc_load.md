# jsdc_load

The `jsdc_load` function is used to load a JSON configuration file into a dataclass object.

## Signature

```python
def jsdc_load(file_path: str, config_class: Type[T]) -> T:
    ...
```

## Parameters

- `file_path` (str): The path to the JSON configuration file to be loaded.
- `config_class` (Type[T]): The dataclass type that the JSON data should be loaded into.

## Return Value

Returns an instance of the specified dataclass (`config_class`) populated with the data from the JSON file.

## Important Notes About Fields

### Using default_factory for Complex Types

When working with complex types (nested dataclasses, enums, etc.), it is required to use `field(default_factory=lambda: ...)` instead of direct default values. This ensures proper initialization and type handling:

```python
from dataclasses import dataclass, field
from enum import Enum

class UserType(Enum):
    ADMIN = "admin"
    USER = "user"

@dataclass
class UserConfig:
    # For enum types, use default_factory
    user_type: UserType = field(default_factory=lambda: UserType.USER)
    
@dataclass
class AppConfig:
    # For nested dataclasses, use default_factory
    user: UserConfig = field(default_factory=lambda: UserConfig())
```

### Why default_factory is Required

- **Type Safety**: Ensures proper initialization of complex types
- **Immutability**: Prevents shared mutable state between instances
- **Serialization**: Guarantees correct JSON serialization/deserialization

## Basic Usage Example

```python
from dataclasses import dataclass
from jsdc_loader import jsdc_load

@dataclass
class DatabaseConfig:
    host: str = 'localhost'
    port: int = 3306
    user: str = 'root'
    password: str = 'password'

# Load configuration from 'config.json'
loaded_db_config = jsdc_load('config.json', DatabaseConfig)
```

## Additional Notes

- The function will automatically convert JSON data types to the appropriate Python types based on the type hints in the dataclass.
- If a field is present in the JSON file but not in the dataclass, it will be ignored.
- If a field is present in the dataclass but not in the JSON file, the default value from the dataclass will be used.
- For complex types (nested dataclasses, enums), always use `field(default_factory=lambda: ...)` to ensure proper initialization.
