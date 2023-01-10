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