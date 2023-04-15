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

