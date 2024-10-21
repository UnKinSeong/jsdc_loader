# Usage

This section provides detailed information on how to use JSDC Loader in your Python projects.

JSDC Loader provides two main functions: `jsdc_load` and `jsdc_dump`. Here's how to use them:

## Loading Configuration

To load a JSON configuration file into a dataclass object:

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
print(loaded_db_config.host)  # Accessing the host attribute from the loaded data
```

## Dumping Configuration

To dump a dataclass object to a JSON file:

```python
from jsdc_loader import jsdc_dump

# Dump configuration to 'config.json'
db_config = DatabaseConfig()
jsdc_dump(db_config, 'config.json')
```

These basic operations allow you to easily manage your configuration data using dataclasses and JSON files.



## See more at [examples](examples/ "mention")

