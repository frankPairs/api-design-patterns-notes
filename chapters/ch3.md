## Chapter 3 - Naming

- An API should could clear names for everyone, including those people that are not developing it.
- Changing a name of a property from the public interface will affect to everyone using it. 
- We can consider that a name is "good" if it has these qualities:
  - **Expressive**. It should be clear to the reader what the thing is representing.
  - **Simple**. We should avoid overcomplicated names but at the same time, we should be careful when in our content there are similar concepts.
  - **Predictable**. Use the same name in your API when we are referring to the same concept.
- Use British English as it is the most common language in Software Development.
- Adapt the API's documentation to the consumers of the API. It is perfectly ok having the documentation in Spanish if most of your client are from Spain.
- Imperative mode provides clarity about what the thing is going to do (HTTP verbs is an example of that with get, create, delete).
- For pluralization, use always the right plural for every word. It does not matter if the word's plural does not follow the 's' rule.
- Avoid using progamming languages to avoid conflicts in the future.
- Keep in mind the API context when creating a new name.
- Don't be obsess using primitives. Sometimes complex data types can express better and clearer what the concept means.