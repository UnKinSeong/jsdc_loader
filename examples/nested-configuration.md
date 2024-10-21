# Nested Configuration Example

This example shows how to work with nested dataclass structures:

```python
from dataclasses import dataclass, field
from jsdc_loader import jsdc_load, jsdc_dump

@dataclass
class UserConfig:
    name: str = 'John Doe'
    age: int = 30

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
print(loaded_app_config.user.name)  # Accessing the name attribute from the loaded data
print(loaded_app_config.database.host)  # Accessing the host attribute from the loaded data
```

This example demonstrates how to create and work with nested dataclass structures, allowing for more complex configuration setups.
