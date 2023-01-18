## Chapter 9 - Custom Methods

- Standard methods should be simple and predictable.
- Custom methods usually use **POST** HTTP method although sometimes could be better using **GET** only when the custom method is idempotent and safe.
- One of the main reasons of creating custom methods is to keep side effects there (like a network request to a third-party service).
    - CreateEmail endpoint creates a draft email (It just interacts with the database).
      - ```POST /api/emails```
    - SendEmail endpoint sends a specific email (it includes a network request to a third-party service)
      - ```POST /api/emails/12345:send```
- A common way to define the path of a custom method is using slashes for representing resources and a colon for representing the action.
  - ```POST /api/emails/1234:send```
- Custom methods should have different paths depending on if we want to perform an action to a resource or to a collection of resources:
  - Send one email -> ```POST /api/emails/1234:send```
  - Remove a bunch of emails -> ```POST /api/emails:delete```
- A custom method does not necessary need to be attached to a resource or a collection. When they are not attached to any resource, they are called **stateless methods**. They are useful for performing computations.
- A stateless method can be attached to a parent resource. In the next example, "text" is just a way to express that we want to return a text translated without saving it.
  - ```POST /api/projects/231/text:translate```
- Custom methods should not be overused, as it will make your API less predictable and more difficult to maintain.
