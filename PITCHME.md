DI Injection and Testing
------------------------

#HSLIDE

Dependency injection is a design pattern that encourages writing decoupled code by passing components and services into a class.

#HSLIDE

*Component*: a local piece of code like a library or another class

*Service*: an external resource like an API or a database

#HSLIDE

Why Decouple
------------
Easier testing, more code portability, separation of concerns

Unit tests and DI promote a virtuous cycle of decoupling code and focusing tests.

#HSLIDE

Setter Injection
----------------

Pass a dependency into a class using a setter method.

Example: An ActiveMQ library might allow you to inject different transports depending on what protocol you want to use to communicate with the server.

    ActiveMQClient amqClient = new ActiveMQClient();
    amqClient.setTransport(new HttpTransport());
    # OR
    amqClient.setTransport(new STOMPTransport());

#HSLIDE

Constructor Injection
---------------------

Pass a dependency into a class in the constructor.

        class UserDAO {
                $dbConnection;
                function __constructor(DbConnection $dbConnection) {
                        // instead of calling new DbConnection() here or having one in $_GLOBALS
                        $this->dbConnection = $dbConnection
                }
        }

#HSLIDE

Let's work through an example

#HSLIDE?gist=eb698ecf38712f53cb04ab54308e08b6

Code example without DI

#HSLIDE

There are some problems here

#HSLIDE?gist=eb698ecf38712f53cb04ab54308e08b6

ContactController and ContactDAO are coupled

#HSLIDE?gist=eb698ecf38712f53cb04ab54308e08b6

ContactDAO has a hard dependency on a specific database library

#HSLIDE?gist=eb698ecf38712f53cb04ab54308e08b6

- Username and password get passed through multiple methods
- Need to copy the same db setup code if I want a OrganizationDAO

#HSLIDE?gist=eb698ecf38712f53cb04ab54308e08b6

How do we test this? We have to have a test db set up, and we have to test the entire endpoint together

#HSLIDE?gist=e83bc582da3064a7a05e2d1b4495fa71

It's pretty hard to unit test even this simple example!

#HSLIDE

Let's try applying some Basic DI to this example

#HSLIDE?gist=9964dc253d13b9497a3424c03e42110e

Code example with basic DI (constructor injection)

#HSLIDE?gist=7ea1c60ad6bb36fb4b7c577e15525ba1

Now we can test the ContactController in isolation and mock the other objects.

#HSLIDE

We've moved some complexity further up the stack.

    $dbConnection = new DatabaseConnection('mysql:host=localhost;dbname=test', $user, $pass);
    $fbAPI = new FacebookAPI($_GLOBALS['fb_api_key']);
    $controller = new ContactController($dbConnection, $fbAPI);

This won't scale very well, especially for classes that are harder to set up.

#HSLIDE

Dependency Injection Frameworks
-------------------------------

DI frameworks exist to organize the code you need to construct your objects,
and to help reduce the amount of boilerplate you need to get an instance.

Most PHP DI is built around the concept of Containers, which is just an object that knows how to
instantiate other objects.

#HSLIDE

Container Interop
-----------------

An emerging standard for defining how containers work in PHP applications.

        interface ContainerInterface {
                // return an instance or configuration parameter
                public function get(String $id);
                // returns True if there is an entry for the identifier
                public function has(String $id);
        }

#HSLIDE?gist=495f2a55c497924dc959f061ae7ba6e4

Containers let you define dependencies and write functions to explain how to create an instance

#HSLIDE 

When to use dependency injection:
 - when you're calling `new Object()` in a constructor
 - when a class needs to call an external service, like a 3rd party API or a database
 - when you're using a class from an external library
 - to decouple implementation and configuration

#HSLIDE

Going forward:
 - How can we remove global-scoped resources?
 - Start using a DI framework in our code?
 - Write unit tests for new code to promote DI and decoupling

#HSLIDE

Further reading:
 - http://fabien.potencier.org/what-is-dependency-injection.html
 - https://www.martinfowler.com/articles/injection.html
 - http://php-di.org/doc/getting-started.html
 - https://github.com/container-interop/container-interop
