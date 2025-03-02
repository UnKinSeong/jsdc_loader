# Working with Optional Fields

This example demonstrates how to use Optional fields in your configurations, allowing for values that may or may not be present.

## Using Optional Types

Python's typing module provides the `Optional` type, which indicates that a value can either be of a specific type or `None`. This is useful for configuration values that aren't always required.

```python
from dataclasses import dataclass, field
from typing import Optional
from jsdc_loader import jsdc_load, jsdc_dump

@dataclass
class ServerConfig:
    host: str = 'localhost'
    port: int = 8080
    
    # Optional fields using default_factory
    username: Optional[str] = field(default_factory=lambda: None)
    password: Optional[str] = field(default_factory=lambda: None)
    
    # You can provide a non-None default for Optional fields if desired
    timeout: Optional[int] = field(default_factory=lambda: 30)

# Create a configuration with default values
config = ServerConfig()
jsdc_dump(config, 'server_config.json')

# Load the configuration
loaded_config = jsdc_load('server_config.json', ServerConfig)

# Check if optional values are set
if loaded_config.username is not None and loaded_config.password is not None:
    print(f"Using authenticated connection with user: {loaded_config.username}")
else:
    print("Using anonymous connection")

# Update optional fields
loaded_config.username = "admin"
loaded_config.password = "secure_password"
jsdc_dump(loaded_config, 'server_config.json')
```

## Important Notes on Optional Fields

1. Always use `field(default_factory=lambda: None)` for Optional fields rather than directly using `None` as a default value.

2. You can check if an Optional field is set using a simple `is not None` comparison:
   ```python
   if config.username is not None:
       # Use the username
   ```

3. Optional fields can be explicitly set to `None` to indicate they aren't used:
   ```python
   config.password = None  # Explicitly disable password
   ```

## When to Use Optional Fields

- For configuration values that aren't always required
- When a configuration setting might be disabled by setting it to `None`
- For fields that should be initialized only when explicitly set

Optional fields provide flexibility in your configuration models, allowing users to specify only the values they need while providing sensible defaults for everything else. 