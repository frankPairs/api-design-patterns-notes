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

- An identifier is used to get a specific resource from a collection of them.
- Properties of a good identifier:
  - **Easy to use**. It can be used as a part of a url, so it takes into account some restrictions (for example, it can't contains slashes)
  - **Unique**. It should be unique in the system. If it is necessary, it could be necessary to make it globally unique althogh those situations are very rare and they require a more complex algorithms.
  - **Permanent**. It should always belong to the same resource. When a resource is removed from the DB, it should not be possible to same its identifier for another one. Like legendary NBA players, their numbers cannot be used anymore after their retirement.
  - **Unpredictable**. It should not use incremental numbers as makes it predicatable for potential attackers. UUIDs, ISBN (for books), or Crackford Base32 can help to make identifiers much more difficult to predict.
  - **Readable, sharable and verifiable**. It should be easy for a user to share it or copy/paste from any device (desktop, mobile phone, or tablet).
  - **Informationally dense**. It should save as much information as into very small space (max. 64 bits)
- How an identifier should look like?:
  - It is an string because string data type provides the highest information density and it makes them easy to use, read and share.
  - Its char encoding format is ASCII. It is better than Unicode because it is more predictable (Unicode allows more than one way to represent the same chunk of text).
  - Its serialization format is Crockford's Base32 as include all the characters to make an identifier readable (a-z, A-Z, 0-9) and a lot of special characters are not part of the format (like slashes).
  - It includes a Checksum. A Checkum is a concatenation of characters that allows us to perform integrity checks. Including them at the end of an indentifier provides us a mechanism to know if the identifier is valid.
  - It represents a specific resource. The most common way to do it is by adding a the resource type separate by a slash (```api/books/abcde-12345-ghjkm-67890```).
  - It could represent a hierarchy relationship between two resources. The child of that relation can only be identify from its parent. For example, if we have a resource called Book an another one called Page where a Book is the **owner** of multiple pages, this would be the way to get a page from a book ```api/books/abcde-12345-ghjkm-67890/pages/2```. It should not be possible to identify a page without specifing its book.
- Identifiers should be generated by the API in order to avoid potential problems like predicability, id collisions or security issues. Although in some situations, it could be convenient or necessary creating them from to the clients. For example, when using a replace standard method (we will talk more about it later).
- They should not be repeated and that applies for removed resources. This requirement can be achieved by:
  - Following a soft delete strategy.
  - Saving all generated ids in a hash map and check them before creation.
- Database storage:
  - In most NoSQL databases, indexing a string field is very fast, so it is perfectly find to save identifiers as string data types.
  - In relational databases, indexing numbers is usually faster than strings. An option could be save an 32/64 bits number although some relational databases work very well with UUIDs identifiers.
- Why not using UUIDs?
  - Very large (128 bits).
  - Less readable and sharable than format like Crockford's Base32.
  - No checksum, although is something we always can add.

# Chapter 7 - Standard methods

- It is easier and more predictable for consumers to use a REST API that is following the standards because .
- All the standard methods of a resource should be available (GET, POST, PUT, PATCH, DELETE). If one of them is not needed or we just do not want to expose it, the API should return a 405 Method Not Allowed response.
- Some methods (like PUT) should be **idempotence**, which means that if a request is executed multiple times using the same paremeters, the response should be the same (assuming no other changes are happening concurrently).
- A standard method should not contain any side effect (like calling an external service or executing an async operation).Manipulating data from the database is not consider as a side-effect. It is not consider like that because the main purpose of an API is providing a way to interact with data resources from the external world.
- Standard methods:
  - **List**
    - It is totally acceptable to return different list of items depending on consumer permissions.
    - Returning the count of the total number of items could be a bad idea. Specially when data can changes very often which will make that count number only real for a short amount of time. In case it is absolutely necessary, this should be documented properly to avoid confusions.
    - It is not recommended to provide a sort mechanism on a standard list method. There are several reasons to avoid it:
      - It can generate performance issues.
      - Resources could potentially come from multiple databases, which would make the operation really complex.
    - Filtering is a common tool APIs offer on a list standard method. An important consideration is that all filters should be strings. They can be parsed later by the API.
  - **Create**
    - Generally, identifiers of new resources should be created by the API. However, some situations could required API clients creating them. This is totally fine although clients should always take into account id format and restrictions.
    - Standard create method has to be strongly consistent. This means that after creation, the new resource should be already available to read, update or delete. When this is not the case (for example, because the resource is created asynchronously), we should use a custom method instead. Remember that standard methods should always have the same behavior in order to provide a predictable API.
  - **Update**
    - Update a resource relies on the PATCH HTTP method.
    - It does a partial update of a resource.
    - They should not include any side-effect (besides interacting with the database). This is important because in some situations we could need to trigger an async operation after updating a specific field/fields of a resource. Those situations should be managed by a custom method instead of a standard update.
  - **Delete**
    - A delete method should not be idempotent, which means that when a resource was already deleted, the right behavior of an API is to return a 404, as the resource does not exist anymore.
  - **Replace**
    - Replace standard method provides a mechanism to replace an entire resource.
    - When a resource does not exist, it should create a new one. Because of that, replace standard method allows consumer of the API to create identifiers.
    - Optional fields from a resource will be deleted if them are not included in the request body.
  - Two kind of APIs:
    - **Imperative API**. Standard methods are focused on their actions. For example, a delete request is considered successful when the delete action was performed successfully. **Resource-oriented APIs are generally imperative**.
    - **Declarative API**. Standard methods are focused on their responses. Same example like before, a delete request will be considered successful even when the resource does not exist.
    - In general, using standard methods following the behaviors exposed is a good idea as it will make your API easier to use.
    - Of course, there are some situations where custom methods are necessary. Just be sure you do not use them because of a bad resource design.

    # Chapter 8 - Partial updates and retrievals
