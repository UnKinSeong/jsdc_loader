# Complex / Nested Configuration

This example shows how to use Enum and other complex types, as long as nested dataclass in your configurations:

```python
from dataclasses import dataclass, field
from enum import Enum, auto
from jsdc_loader import jsdc_load, jsdc_dump

class UserType(Enum):
    ADMIN = auto()
    USER = auto()

@dataclass
class UserConfig:
    name: str = 'John Doe'
    age: int = 30
    married: bool = False
    user_type: UserType = field(default_factory=lambda: UserType.USER)

@dataclass
class DatabaseConfig:
    host: str = 'localhost'
    port: int = 3306
    user: str = 'root'
    password: str = 'password'

@dataclass
class AppConfig:
    user: UserConfig = field(default_factory=lambda: UserConfig())
    database: DatabaseConfig = field(default_factory=lambda: DatabaseConfig())

# Dump configuration to 'config.json'
app_config = AppConfig()
jsdc_dump(app_config, 'config.json')

# Load configuration from 'config.json'
loaded_app_config = jsdc_load('config.json', AppConfig)
print(loaded_app_config.user.user_type)  # Accessing the user type attribute from the loaded data
print(loaded_app_config.user.married)  # Accessing the boolean attribute from the loaded data
```

This example demonstrates how to use Enum types and boolean values in your dataclass configurations, as well as the nested assignment, showing JSDC Loader's ability to handle more complex data types.
