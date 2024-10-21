# Simple Configuration Example

This example demonstrates how to use JSDC Loader with a simple configuration:

```python
from dataclasses import dataclass
from jsdc_loader import jsdc_load, jsdc_dump

@dataclass
class DatabaseConfig:
    host: str = 'localhost'
    port: int = 3306
    user: str = 'root'
    password: str = 'password'

# Dump configuration to 'config.json'
db_config = DatabaseConfig()
jsdc_dump(db_config, 'config.json')

# Load configuration from 'config.json'
loaded_db_config = jsdc_load('config.json', DatabaseConfig)
print(loaded_db_config.host)  # Accessing the host attribute from the loaded data
```

This example shows how to define a simple dataclass for database configuration, dump it to a JSON file, and then load it back into a dataclass object.
