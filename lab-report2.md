# Part 1
![Image](/lab-report2-images/hello.png)

* When the above input is given, first the `main()` method runs, which checks that a port number is given as a command line argument, reads the port, and starts the server. The other method in my code that runs is `handleRequest()` in the `Handler` class, which takes a URL argument called `url`. In this case, the url is `http://localhost:4000/add-message?s=Hello!&user=kiran`. 
* The intial value of `str`, which is the `String` field of the `Handler` class, is an empty `String`. 
* The `handleRequest()` method then splits the query of `url` into its relevant parts and updates `str` with the query of the url formatted according to the specified format. In this case, the value of `str` becomes `"kiran: Hello!"`. The `handleRequest()` method then returns `str`.

![Image](/lab-report2-images/hello-hey-there.png)
* When the above input is given, first the `main()` method runs, which checks that a port number is given as a command line argument, reads the port, and starts the server. The other method in my code that runs is `handleRequest()` in the `Handler` class, which takes a URL argument called `url`. In this case, the url is `http://localhost:4000/add-message?s=Hey there!&user=other kiran`.
* The field `str` of type `String` initially has a value of `kiran: Hello!\n` from the last query made.
* The `handleRequest()` method then splits the query of `url` into its relevant parts and updates `str` with the query of the url formatted according to the specified format. In this case, the value of `str` becomes `"kiran: Hello!\nother kiran: Hey there!"`. The `handleRequest()` method then returns `str`.

How does the `handleRequest()` method split the query into its relevant parts? We know that the message and user in the query will be separated by a `'&'`, so the method splits at that character and assigns it to a `String` array. Then, both the message and the name will have an equals sign (`'='`) that separates the relevant part. By splitting at `'='` for both and assigning the corresponding parts to a `name` and `message` variable, we have all the parts we need to format the `String` to update `str` and for the function to return. 

# Part 2


Path to private key: /Users/separate/.ssh/id_rsa  
Path to public key: /Users/separate/.ssh/id_rsa.pub

