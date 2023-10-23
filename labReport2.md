# Part 1

## Code for StringServer.java
![CSE15Lab2pic2](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/25e1d21e-b8f1-4851-b18e-9e111bde9c73)

## First screenshot for 1. Hello                               
![CSE15Lab2pic3](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/b405a7e9-6b31-4f1b-aae9-7e2aa1a970b2)
* The main method and the handleRequest method are used in the code. Within the main method, the Server.start method starts the server. 
* For the main method, the argument `args` array is checked to see if it contains the port number. For my Server, the value of my port number is 4000. For the handleRequest method, the `url` argument represents the URI of the HTTP request and determines the path and query of that request. 
My first request is `/add-message?s=Hello`. The value of the `count` integer field is initialized as 0 and the value of `message` string field is initialized as an empty string.
* After this first request, the `count` field is incremented by 1, and the `message` field updates to 1. Hello. 

## Second screenshot for 1. Hello and 2. How are you
![CSE15Lab2pic4](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/c191b3b7-e730-43df-b6ad-35ce49d62278)
* Since the server has already started, a new request would only call the handleRequest method.
* The relevant `url` argument to this method is my second request `/add-message?s=How are you`. Before the second request, the `count` field is 1 and `message` is 1. Hello. 
* From this specific request, the `count` will be incremented by 1 again so now it's 2, and `message` updates the new message to 1. Hello 2. How are you.

# Part 2

Path to the private key for SSH key                    
![CSE15Lab2pic5](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/fe91e785-df72-4bfa-8c6d-423e0f8d5406)

Path to the public key for SSH key                      
![CSE15Lab2pic8](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/4cfc439f-e8c0-4d2e-ad3d-0cd1dceadd65)

Terminal interaction to log into ieng6
![CSE15Lab2pic6](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/3e3b191c-ed21-44cb-a354-5411e15c8a8d)
![CSE15Lab2pic7](https://github.com/clarissacheng/cse15l-lab-reports/assets/112114163/aa7bca59-cfc6-42bd-8883-a4b15e6c1b2f)

# Part 3

Something I learned from week 3 was that the `man` command allows you to look up the functions of other commands. For example, `scp` means secure copy and allows you to copy files between hosts on a network. `Mkdir` means make directories and allows you to create directories if they don't already exist.

