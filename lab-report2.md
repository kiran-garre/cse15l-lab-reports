# Part 1
Chat server code:  
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {

    String str = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/add-message")) {
            String[] user_and_message = url.getQuery().split("&");
            String message = user_and_message[0].split("=")[1];
            String user = user_and_message[1].split("=")[1];

            str += String.format("%s: %s\n", user, message);
        }
        return str;
    }
}

class ChatServer {
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
To start the server, we first compile the file and then run `java ChatServer 4000`. This specifies the port number as 4000 (we can choose other port numbers too). The `main()` method runs and checks that a port number is given as a command line argument. In this case, the port number 4000 is assigned to the `int` variable `port`. The `Server.start()` method is then called with the `port` value and a new `Handler()` object.

![Image](/lab-report2-images/hello.png)

* When the above input is given, the method in my code that runs is `handleRequest()` in the `Handler` class, which takes a URL argument called `url` (which is a `URI` object). In this case, the URL is `http://localhost:4000/add-message?s=Hello!&user=kiran`. The `URI` object calls two instance methods, `getPath()` and `getQuery()`, which return the path and query of the URL respectively.
* The intial value of `str`, which is the `String` field of the `Handler` class, is an empty `String`. 
* The `handleRequest()` method then splits the query of `url` into its relevant parts and updates `str` with the query of `url` formatted according to the specified format. In this case, the value of `str` becomes `"kiran: Hello!\n"`. The `handleRequest()` method then returns `str`.

![Image](/lab-report2-images/hello-hey-there.png)
* When the above input is given, the method in my code that runs is `handleRequest()` in the `Handler` class, which takes a URL argument called `url` (which is a `URI` object). In this case, the URL is `http://localhost:4000/add-message?s=Hey there!&user=other kiran`. The `URI` object calls two instance methods, `getPath()` and `getQuery()`, which return the path and query of the URL respectively.
* The field `str` of type `String` initially has a value of `"kiran: Hello!\n"` from the last query made.
* The `handleRequest()` method then splits the query of `url` into its relevant parts and updates `str` with the query of `url` formatted according to the specified format. In this case, the value of `str` becomes `"kiran: Hello!\nother kiran: Hey there!\n"`. The `handleRequest()` method then returns `str`.

How does the `handleRequest()` method split the query into its relevant parts? We know that the message and user in the query will be separated by a `'&'`, so the method splits at that character and assigns it to a `String` array. Then, both the message and the name will have an equals sign (`'='`) that separates the relevant part. By splitting at `'='` for both and assigning the corresponding parts to a `name` and `message` variable, we have all the parts we need to format the `String` to update `str` and for the function to return. 

# Part 2
Paths to private and upblic keys using `ls`:
![Image](/lab-report2-images/key_paths.png)

Absolute path to private key: `/Users/separate/.ssh/id_rsa`  
Absolute path to public key: `/Users/separate/.ssh/id_rsa.pub`

Logging in without password: 
![Image](/lab-report2-images/login-without-password.png)




