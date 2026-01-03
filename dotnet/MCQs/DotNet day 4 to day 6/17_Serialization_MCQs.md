# 17_Serialization – MCQs

## EASY MCQs

### Q1. What is the process of converting an object into a portable format called?
A. Parsing  
B. Serialization  
C. Encoding  
D. Encryption  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Serialization saves the state of an object into a stream/buffer (JSON, XML, Binary) so it can be stored or transmitted.
</details>

### Q2. Which namespace contains the modern JSON serializer in .NET?
A. `System.Json`  
B. `System.Text.Json`  
C. `Newtonsoft.Json`  
D. `System.Web.Script.Serialization`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
`System.Text.Json` (introduced in .NET Core 3.0) is the high-performance, built-in library for JSON handling.
</details>

### Q3. Which attribute prevents a property from being serialized to JSON?
A. `[NonSerialized]`  
B. `[JsonIgnore]`  
C. `[IgnoreDataMember]`  
D. `[Hide]`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
When using `System.Text.Json`, `[JsonIgnore]` marks a property to be skipped during serialization/deserialization.
</details>

### Q4. The reverse process of recreating an object from data is:
A. Deserialization  
B. Decoding  
C. Unboxing  
D. Rehydration  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Deserialization is extracting the data structure from the serialized format (like a JSON string) and reconstructing the object in memory.
</details>

### Q5. Why is `BinaryFormatter` discouraged?
A. It is too slow.  
B. It produces large files.  
C. It is insecure and deprecated (security risk).  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
`BinaryFormatter` allows arbitrary code execution during deserialization, making it a critical security vulnerability ("insecure deserialization"). It is marked Obsolete in newer .NET versions.
</details>

---

## MEDIUM MCQs

### Q6. To customize the property name in the generated JSON, use:
A. `[DisplayName("name")]`  
B. `[JsonPropertyName("name")]`  
C. `[JsonName("name")]`  
D. `[Column("name")]`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
The `[JsonPropertyName]` attribute maps a C# naming convention (PascalCase) to a different JSON naming convention (e.g., snake_case or camelCase) specifically for that property.
</details>

### Q7. `JsonSerializer.Deserialize<T>(jsonString)` requires `T` to have:
A. A public parameterless constructor.  
B. `[Serializable]` attribute.  
C. Only string properties.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Most serializers (including System.Text.Json) instantiate simple DTOs by calling the default constructor and then setting properties. (Though newer versions support constructor parameter matching, the default constructor is the standard requirement).
</details>

### Q8. Which format is typically most compact and fastest for machine-to-machine communication?
A. XML  
B. JSON  
C. Protocol Buffers (Binary)  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
Binary formats like Protobuf are significantly smaller and faster to parse than text-based formats like JSON or XML because they skip the text encoding/decoding overhead.
</details>

### Q9. If a JSON field is missing during deserialization, the corresponding C# property will be:
A. `null` (or default value).  
B. The deserialization throws an Exception.  
C. Skipped but keeps its old value.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Standard behavior is permissive. If the JSON property is missing, the C# property remains at its default value (null for objects, 0 for int).
</details>

### Q10. How do you handle circular references in `System.Text.Json`?
A. Use `ReferenceHandler.Preserve` in `JsonSerializerOptions`.  
B. Use `[JsonCircular]` attribute.  
C. It is impossible; stack overflow always occurs.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
By default, circular references throw an exception. Setting `ReferenceHandler.Preserve` enables metadata ($id, $ref) to track object references to serialize/deserialize cyclic graphs correctly.
</details>

---

## HARD MCQs

### Q11. Which attribute is used for XML Serialization to rename the root element?
A. `[XmlRoot("Name")]`  
B. `[XmlElement("Name")]`  
C. `[DataContract("Name")]`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
The `XmlSerializer` uses `[XmlRoot]` to control the name of the top-level XML element.
</details>

### Q12. `JsonSerializerOptions.WriteIndented = true` generates:
A. Minified JSON.  
B. Pretty-printed (formatted) JSON.  
C. Binary JSON.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It adds whitespace and newlines to make the output string human-readable, at the cost of larger payload size.
</details>

### Q13. `[JsonInclude]` is used to:
A. Include public properties.  
B. Force inclusion of non-public properties.  
C. Include static fields.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
By default, serializers only look at public properties. `[JsonInclude]` allows you to opt-in specific private or protected properties for serialization.
</details>

### Q14. Can you serialize a `Dictionary<string, int>` to JSON?
A. Yes, it becomes a JSON object.  
B. No, Dictionaries are not supported.  
C. Yes, it becomes a JSON array.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
A Dictionary with string keys maps naturally to a JSON object: `{"key1": 1, "key2": 2}`.
</details>

### Q15. `JsonIgnoreCondition.WhenWritingNull` means:
A. The property is ignored if the value is null during serialization.  
B. Attempting to deserialize null checks throws an error.  
C. Null values are written as "null" string.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
This option reduces payload size by omitting keys entirely if their value is null, rather than sending `"key": null`.
</details>
