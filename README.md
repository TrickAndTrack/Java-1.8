# Java-1.8
Oracle released a new version of Java as Java 8 in March 18, 2014.
# Java 8 provides following features for Java Programming:

1. Lambda expressions,
2. Method references,
3. Functional interfaces,
4. Stream API,
5. Default methods,
6. Base64 Encode Decode,
7. Static methods in interface,
8. Optional class,
9. Collectors class,
10. ForEach() method,
11. Nashorn JavaScript Engine,
12. Parallel Array Sorting,
13. Type and Repating Annotations,
14. IO Enhancements,
15. Concurrency Enhancements,
16. JDBC Enhancements etc.


## Lambda expressions
Java 8 Lambda Expressions can be defined as methods without names i.e., anonymous functions.  It saves a lot of code.It is very useful in the collection library. It helps to iterate, filter, and extract data from the collection.
To provide the implementation of a Functional interface.
Less coding.
Removes verbosity and repetition of code.
You to write more clear, concise, and flexible code.

## Lambda Syntax
No Parameter Syntax ->  () -> {  
                                //Body   
                                }  
One Parameter Syntax -> (p1) -> {  
                                //Body 
                                }  
Two Parameter Syntax ->  (p1,p2) -> {  
                                    //Body multiple 
                                    }  

### What are the three main parts of a Lambda expression in Java?
1)	Parameter list
2)	Lambda arrow operator: -> It separates the list of parameters and the body of Lambda.
3)	Lambda expression body: The piece of code that we want to execute is written in the Lambda expression body.

### Where to Use Lambda Expressions?
Lambda expressions are used where an instance of the functional interface is expected.Functional interfaces can have any number of default methods. But, they must have only one abstract method

### What is the data type of a Lambda expression? -> The data type of a Lambda expression is a Functional interface.

### how lambda expressions can be used with CRUD (Create, Read, Update, Delete) operations:
```java
public class User {
    private int id;
    private String name;
    private int age;

    // constructors, getters, and setters
}
READ:
```java
// Get all users whose age is greater than or equal to 18
List<User> adultUsers = userList.stream()
                                .filter(u -> u.getAge() >= 18)
                                .collect(Collectors.toList());

// Get the user with id = 1
Optional<User> userOptional = userList.stream()
                                      .filter(u -> u.getId() == 1)
                                      .findFirst();
User user = userOptional.orElse(null);

=========================================API With Java1.8================================================================== 
 @GetMapping("/{id}")
    public User getUser(@PathVariable Long id) {
        return users.stream()
                    .filter(user -> user.getId().equals(id))
                    .findFirst()
                    .orElseThrow(() -> new ResponseStatusException(HttpStatus.NOT_FOUND, "User not found"));
    }
    
    @GetMapping
    public List<User> getUsers() {
        return users;
    }



```
UPDATE:
```java
// Update the age of the user with id = 1
userList.stream()
        .filter(u -> u.getId() == 1)
        .findFirst()
        .ifPresent(u -> u.setAge(30));
        
        
=========================================API With Java1.8==================================================================        
 
   @PutMapping("/{id}")
    public User updateUser(@PathVariable Long id, @RequestBody User user) {
        User oldUser = users.stream()
                            .filter(u -> u.getId().equals(id))
                            .findFirst()
                            .orElseThrow(() -> new ResponseStatusException(HttpStatus.NOT_FOUND, "User not found"));
        
        oldUser.setName(user.getName());
        oldUser.setAge(user.getAge());
        
        return oldUser;
    }
```
DELETE:

```java
// Delete the user with id = 1
userList.removeIf(u -> u.getId() == 1);


=========================================API With Java1.8================================================================== 
@DeleteMapping("/{id}")
    public void deleteUser(@PathVariable Long id) {
        boolean removed = users.removeIf(user -> user.getId().equals(id));
        if (!removed) {
            throw new ResponseStatusException(HttpStatus.NOT_FOUND, "User not found");
        }
    }
```
# Java Functional Interfaces
•	What is a Functional interface in Java 8?
•	What is a Single Abstract Method (SAM) interface in Java 8?
•	How can we define a Functional interface in Java 8?
•	Why do we need Functional interface in Java? ->mainly used in Lambda expressions, Method references, and constructor references.
•	What are the differences between Predicate, Supplier, and Consumer in Java 8?

An Interface that contains exactly one abstract method is known as a functional interface. They may have any number of default methods but must have only one abstract method. Functional interfaces provide only one functionality to implement.

Let’s see how to use 4 important functional interfaces	          Functional Interfaces Supporting Primitive Type
| |  ||
| ------------- | ------------- |------------- | 
| Predicate  | Boolean result  |IntPredicate,LongPredicate, double Predicate|
| Consumer  | No Result  |IntConsumer,LongConsumer, double Consumer |
| Function  | Input and output  |IntFunction,LongFunction, doubleFunction,  toIntFunction, toLongFunction, todouble Function |
| Supplier  | No input only supply  |IntSupplier,LongSupplier,doubleSupplier |
