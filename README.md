# API Design Patterns - Notes

Notes and reflections while reading [API Design Patterns by JJ Geewax](https://www.manning.com/books/api-design-patterns).

## Chapter 1 - Introduction to API's

- An API defines interfaces where computers can "speak" between them in an easy way.
- Stateless and Stateful API's:
  - API call is considered stateless when is independent from other API requests and does not need additional context. For example, and API that expects 2 numbers and it returns the sum of them.
  - API call is considered stateful when it us dependent of other API requests or needs previosly stored data. For example, a call that returns the weather forecast of users' favorite cities. In that case, you need data stored previously in the database (users and cities) to return the expected response.
- API resource-oriented:
  - It manages API's based on resources. They are entities/objects with a relevant meaning for the context we are working on. Commonly we store and interact with them.
  - It defines a standard set of actions (create, delete, update, get) to interact with each resource.
  - This API design makes it easy to learn for new developers and very predictable.
- API can be considered good when:
  - It is **operational**. It does what users want and expect.
  - It is **expressive**. It provides mechanisms for users to clearly express what they want.
  - It is **simple**. It exposes the functionality that users want in the easiest possible way.
  - It is **predictable**. It applies well-known, well-define and simple patterns which are predictable and easy to learn.

  ## Chapter 2 - Introduction to API design patterns

  - Design patterns focus on specific components rather than entire systems.
  - There are two important aspects when we are designing an API: *flexibility* and *visibility*.
    - An API is flexible when accomodate changes is easy. Rigid designs are difficult to changes which means we have to carry on with the decisions made in the past.
    - Every API has public parts (the ones accessible by users) and private parts (implementation details that are hidden and not accessible). We can change private parts of our API as far as we keep the same public interfaces.

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

## Chapter 5 - Data types and defaults

- Serialization vs deserialization.
  - **Serialization** is converting from language data representation to language-agnostic representation (eg: JSON, XML).
  - **Deserialization** is converting language-agnostic representation to language data representation (eg: from Rust struct to JSON).
- Boolean data type.
  - Zero value is *false*.
  - Positive names are easier to understand than negative ones (eg: **allowedNumbers** vs **disallowedNumbers**)
- Number data type.
  - Zero value is *0* or *0.0*. 
  - Number data types should be used when we expect clients of the API to do any kind of arithmetic operation with the field's value. For example, using numbers for ids is not a good fit.
  - Serialize number data types to string could be an option for avoiding mismatches when client's programming language does not have appropiate native representation.
- String data type.
  - Zero value is *""*.
  - An API should use UTF-8 encoding format unless there is any special reason not to do it.
  - In order to create a predictable API, we should reject any string that exceed the size limit or that are not using the expected encoding format.
- Enumeration data type.
  - Advantages of using enumeration data type:
    - Easier validation.
    - Compresion because its data representation is usually using numbers instead of strings.
  - API requests and responses should avoid use enumerations. In order to provide a better readibility, strings is a more convenient data type.
- List data type.
  - It should be atomic, which means that if one item of the list needs to be update, the entire list should be replaced.
  - It should not be possible to update a list field from a resource. For example, if we have a resource called Book where Book.categories is a list, book categories cannot be update using the Book resource API. Instead, we should use the Category resource API.
  - It should have a size limit in order to avoid potential performance issues, specially when the resource can grow dynamically. Pagination is one of the mechanism to control the size of a list field from an API response.
- Map data type.
  - Two kind of data types:
    - **Custom data types maps** contain well defined fields and their types.
    - **Dynamic data types maps** are dynamic data structures where we don't know their fields. These kind of maps are very useful for saving arbitrary data.
  - In case of dynamic maps, it is important to bound the size of map's keys and values (for example, a key cannot contain more than 50 characters).

## Chapter 6 - Resource identification