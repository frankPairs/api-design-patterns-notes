## Chapter 2 - Introduction to API design patterns

- Design patterns focus on specific components rather than entire systems.
- There are two important aspects when we are designing an API: *flexibility* and *visibility*.
  - An API is flexible when accomodate changes is easy. Rigid designs are difficult to changes which means we have to carry on with the decisions made in the past.
  - Every API has public parts (the ones accessible by users) and private parts (implementation details that are hidden and not accessible). We can change private parts of our API as far as we keep the same public interfaces.