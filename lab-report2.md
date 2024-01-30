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
Path to private key using `ls` on local computer:
![Image](/lab-report2-images/private-key-path.png)

Absolute path to private key: `/Users/separate/.ssh/id_rsa`  

Path to public key on `ieng6` filesystem:  
![Image](/lab-report2-images/public-key-path.png)
  
Absolute path to public key: `/home/linux/ieng6/oce/59/kgarre/authorized_keys`

Logging in without password: 
![Image](/lab-report2-images/login-without-password.png)

# Part 3
One thing I learned in lab during weeks 2 and 3 was that you can easily login to another computer using `ssh`. I never knew that it was so simple to remotely login (since it only takes one command; I thought it would be a much more involved process, something you might see hackers or cybersecurity experts doing). I am very interested to see what other functionalities `ssh` can offer and how this might be used in a professional setting in the future.




