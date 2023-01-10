## Chapter 4 - Resource scope and hierarchy

- When we talk about a resource, we mean:
  - Arrangement of resources or "things" in our API.
  - Its fields describes their properties.
  - Relationships between them.
- Hierarchical relationships tend to reflect the containment or ownership between resources.
- Hierarchical relationships make sense when a child resource can have only one parent, like the relationship between a folder and a file.
- Before creating an API resource relationship, be sure that is really necessary.
- In-line vs in-reference data, when should use each of them? Depends on how often you think data is going to be necessary and the structure of them:
  - In-line data should be use when data is not complex and it is going to be necessary for clients very often.
  - In-reference data should be use when data is complex and it is not going to be requested very often by clients.
- Not everything in an API is a resource. Creating unnecessary resources can end up with deep hierarchies which will make more difficult the interaction between your clients and the API.
  - Things that are always related to the same resource can be defined as data types.
  - Do you need to interact with a resource in isolation? Or it is always linked to another one? Answering those questions can provide you a hint of if a resource is really necessary.
