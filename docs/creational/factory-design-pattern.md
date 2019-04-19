## Factory Design Pattern

A pattern used to simplify object creation. Creating different objects based on need is very easy in the factory design pattern. 

Let's say we have a repositiry to perform the database related operations. So we can create a Repository Factory that handle all the things controller or route does not need to know all those things in repository.

We can list all the respositories in the repository factory and return required the repository during the function call.