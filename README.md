# CubeSocket
Socket bindings using the Cube90 cipher for encryption and decryption

# Description
CubeSocket provides two classes CubeSocket and CubeWrap.  CubeSocket is used like the ordinary socket calls but the are encapsulated with the Cube90 cipher.  CubeWrap is used to encapulate an existing socket.

The cubesend and cuberecv methods can be used to securely transmit messages to and from a server.  They cubesend method generates a one time use 16 character key, encrypts it with the session key and then encrypts the payload with the one time key.  The cubeconnect method must be called first before using cubesend or cuberecv.

The cubeconnect utilizes a pre-shared key to exchange a random 16 character session key with the server and then proceeds using the session key.

A socket can be utilized directly without a secure handshake by calling CubeSocket's connect method.  The key must be known on either end.

Supports ASCII characters 32-90

# Prerequisites
pycube90

# Client Example

key = "Test"  
sock = CubeSocket(key)  
sock.cubeconnect("localhost", 99)  
sock.cubesend("Test")  
sock.close()  

# Server Example

host = "localhost"  
port = 99  
sock = CubeSocket("Test")  
sock.bind(host, 99)  
sock.listen(1)  
client, addr = sock.accept()  
cubesock = CubeSocket(client, sock.key)  
test = cubesock.sock.cuberecv(32)  
print test  
c.close()  
sock.close()  

# CubeWrap Example

cubesock = CubeSocket(sock, key)  
test = cubesock.sock.recv(32)  

# UDP client example

from CubeSocket import CubeSocket  

host = "localhost"  
port = 1666  

socket = CubeSocket("NEVER", nonce_support=1,  mode=1)  
socket.cubesendto("HELLO", host, port)  

# UDP Server example

from CubeSocket import CubeSocket

host = "localhost"  
port = 1666  

socket = CubeSocket("NEVER", nonce_support=1, mode=1)  
socket.bind(host, port)  
while True:  
    data = socket.cuberecvfrom(1024)  
    print data  
