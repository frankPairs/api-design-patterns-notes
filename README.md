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