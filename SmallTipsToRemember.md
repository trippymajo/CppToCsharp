# Encrypting large data
When it comes to encrypting large data, you should consider first compressing it then encrypting. In order 
to gain performance.  
Example:
string -> StreamWriter -> GZipStream -> CryptoStream -> FileStream -> file
  
# Dealing with XML
  
| Feature            | System.Xml (`XmlDocument`) | System.Linq.Xml (`XDocument`) |
|--------------------|--------------------------|------------------------------|
| **Programming Model** | DOM-based (imperative) | LINQ-based (functional) |
| **Performance** | Slower for modifications | Faster and optimized for queries |
| **Ease of Use** | Verbose, requires more code | Concise and readable |
| **Best for** | Large files, streaming, validation | Querying, modifying small-to-medium XML |
| **Querying** | XPath (`SelectSingleNode`) | LINQ (`doc.Element()`) |
| **Writing XML** | `XmlWriter`, manual DOM creation | Fluent API (`XElement`, `XAttribute`) |
| **Streaming Support** | Yes (`XmlReader`) | No (entire XML is loaded into memory) |
| **Validation Support** | Supports XSD validation (`XmlSchema`) | No built-in validation |
| **Modification Performance** | Expensive (modifies DOM directly) | Optimized for element-level updates |
| *
  
# Dealing with JSON
  
| Feature            | System.Text.Json (`JsonSerializer`) | Newtonsoft.Json (`JsonConvert`) |
|--------------------|----------------------------------|--------------------------------|
| **Namespace** | `System.Text.Json` | `Newtonsoft.Json` |
| **Serialization Speed** | Faster (optimized for performance) | Slightly slower due to more features |
| **Deserialization Speed** | Faster | Slightly slower |
| **Ease of Use** | Requires explicit property names (`JsonPropertyName`) | Supports both attributes and dynamic parsing |
| **Built-in Support** | .NET Core 3.0+ and .NET 5+ | External NuGet package required |
| **Memory Efficiency** | More efficient, avoids excess allocations | Higher memory usage |
| **Streaming Support** | Yes (`Utf8JsonReader`, `Utf8JsonWriter`) | Yes (`JsonTextReader`, `JsonTextWriter`) |
| **Case Insensitivity** | No (strict by default, can be configured) | Yes (default behavior) |
| **LINQ to JSON** | No native support | Yes (`JObject`, `JArray`) |
| **Reference Handling** | Limited (`ReferenceHandler.Preserve`) | Full support (`PreserveReferencesHandling`) |
| **Circular Reference Handling** | Partial support (not as flexible) | Full support |
| **Custom Converters** | Requires implementing `JsonConverter<T>` | Supports `JsonConverter` and many built-in converters |
| **JSON Schema Validation** | No | Yes |
| **Comments in JSON** | Not supported | Supported (`AllowComments` setting) |
| **Missing Property Handling** | Throws exception unless configured | Supports `NullValueHandling` and `MissingMemberHandling` |
| **Date Handling** | Strict ISO 8601 format | Flexible date formats (`DateFormatHandling`) |
| **Polymorphic Deserialization** | Limited support | Fully supported |
| **Third-Party Integration** | Less supported due to newer API | Widely supported in libraries |
