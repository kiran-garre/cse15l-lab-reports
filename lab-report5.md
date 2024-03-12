## Original post:
Hello! I am trying to implement a method a case in my `NumbeServer.java` file where a user can increment `num` by a variable amount (rather than just incrementing by 1).
Here is my code:
Here is a symptom of the `num` variable not incrementing:
Here, I am trying to add 10 to `num` and display it, but `num` is not increasing. I think this is an issue with my query splitting, but I'm not sure. 
It seems like any query with the path `/add` isn't working. 

## TA Answer:
Hey there! It looks like there's an issue with your `if` statements where you choose the corresponding behavior for each path. Trace through the conditionals when you use the `/add` path, and consider which statements execute and 
which don't. It may also be helpful to read the documentation for the `String` `contains()` method you use in your `if` statements.

## Student response:
Hello! I traced through my code and figured out the issue: using `contains()` in my `if` statement would cause that block to run (since the `/add` query contains the `"/"` character), and then it would skip the rest of the `else if` 
and `else` blocks. Instead, using the `equals()` method gave me the correct output. 
New code: 
New output:


#### File structure:
├── server-folder
│   ├── NumberServer.java
│   ├── Server.java
│   ├── run-number-server.java
│   ├── URLHandler.class
│   ├── ServerHttpHandler.class
│   ├── Handler.class

#### Contents of `NumberServer.java` __before__ fixing the bug:
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    int num = 0;

    public String handleRequest(URI url) {
        if (url.getPath().contains("/")) {
            return String.format("Number: %d", num);
        } else if (url.getPath().equals("/increment")) {
            num += 1;
            return String.format("Number incremented!");
        } else {
            if (url.getPath().contains("/add")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("count")) {
                    num += Integer.parseInt(parameters[1]);
                    return String.format("Number increased by %s! It's now %d", parameters[1], num);
                }
            }
            return "404 Not Found!";
        }
    }
}

class NumberServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
#### Contents of `run-number-server.sh` __before__ fixing the bug:
```
javac NumberServer.java Server.java
java NumberServer 4000
```

#### Contents of `NumberServer.java` __after__ fixing the bug:
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    int num = 0;

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("Number: %d", num);
        } else if (url.getPath().equals("/increment")) {
            num += 1;
            return String.format("Number incremented!");
        } else {
            if (url.getPath().contains("/add")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("count")) {
                    num += Integer.parseInt(parameters[1]);
                    return String.format("Number increased by %s! It's now %d", parameters[1], num);
                }
            }
            return "404 Not Found!";
        }
    }
}

class NumberServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
#### Contents of `run-number-server.sh` __after__ fixing the bug:
```
javac NumberServer.java Server.java
java NumberServer 4000
```

#### Commands to produce the bug:
```
$ bash run-number-server.sh
```
which then runs the commands `javac NumberServer.java Server.java` and `java NumberServer 4000` found in `run-number-server.sh`

#### Edit made: 
I changed the `contains()` method to `equals()` in my `if` statement on line 10 of `NumberServer.java` so that the `/add` query would go to the `else` block on line 15 rather than skipping it.




