###Tutorial for recreating state learner from “Protocol State Fuzzing of TLS Implementations”

**Download repository from github**

Create a folder and git clone repository from GIthub 
Execute    git clone https://github.com/jderuiter/statelearner

**Install TLS implementations** 
It depends on what kind of implementations you wanna run, the paper tested 9 TLS implementations, here we pick most common one, OpenSSL as an example. 

Install OpenSSL

```
sudo apt-get install openssl
```

**Install maven**

If you already installed maven, ignore this step. 
The repository is managed by using Maven. 
Execute 

```
sudo apt-get install maven.
```

**Build jar file**
Execute 

```
mvn package shade:shade 
```

To build up a self-contained jar file

**Run TLS implementation**

Since we want to fuzz TLS implementation. We can go to examples/openssl/ folder, and run openssl server with the following command:

```
openssl s_server -key server.key -cert server.crt -CAfile cacert.pem -
accept 4433 -HTTP
```

In this example, key is in server.key file, certificate in server.crt. Port localhost:4433 is used for OpenSSL. You can use execute command netstat -natp to check if your server implementation is running.

**Run Learner**

We advise you to use IDE running Learner. Open statelearner project in your IDE. <b>You are required to define a parameter as an argument in your command for running it.</b> It should be a <b>properties</b> file. One way is moving all files from statelearner/examples/openssl to statelearner/
Always declare server.properties as an argument in your command running learner. 

**Result**

Learner always create a folder called ouput_server and automatically save all results to it. The version of my OpenSSL is 1.0.1t. Learner learnt two hypothesis and you can check the pdf of them. 

<p align="center"><img src="hypothesis_1.dot.pdf" height="300" width="700">
<p align="center"><img src="hypothesis_2.dot.pdf" height="300" width="700">

The input alphabe for this example is 

```
ClientHelloRSA ClientHelloDHE EmptyCertificate ClientKeyExchange ChangeCipherSpec Finished ApplicationData ApplicationDataEmpty Alert10
```
It has been predefined at alphabet in the file of server.properties
 
