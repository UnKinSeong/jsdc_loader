# Examples

This section provides practical examples of how to use JSDC Loader in various scenarios. Each example demonstrates a specific aspect of the library, from basic usage to handling more complex configurations.

## Available Examples

### [Simple Configuration](simple-configuration.md)
A basic example showing how to create, save, and load simple configurations with primitive types (strings, integers, booleans).

**Key concepts covered:**
- Creating dataclass models for configuration
- Setting default values for configuration options
- Loading and saving configurations
- Accessing configuration values

### [Enum and Complex Types](enum-and-complex-types.md)
A more advanced example demonstrating how to work with Enum types, nested dataclasses, and complex configuration structures.

**Key concepts covered:**
- Using Enum types for configuration options with fixed choices
- Creating hierarchical configuration with nested dataclasses
- Proper use of `default_factory` for complex types
- Loading and modifying complex configurations

## When to Use Which Pattern

- **Simple Configuration**: Use when your configuration needs are straightforward with mostly primitive types and minimal nesting.
- **Complex Configuration**: Use when you need to model configuration with hierarchical structure, enums for choice validation, or more complex relationships.

## Additional Examples

We're continuously adding more examples to demonstrate various use cases. Some upcoming examples may include:

- Working with Optional fields
- Configuration validation patterns
- Handling configuration versioning
- Using JSDC Loader with environment variables

If you have a specific example you'd like to see, please consider [contributing](../contributing.md)!
