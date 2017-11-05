# CubeSocket256
Socket bindings using the Cube256 cipher for encryption and decryption

# Description
CubeSocket provides two classes CubeSocket and CubeWrap.  CubeSocket is used like the ordinary socket calls but the are encapsulated with the Cube256 cipher.  CubeWrap is used to encapulate an existing socket.

By default CubeSocket uses DiffieHellman Ephemeral to establish a shared secret. After which Cube256 cipher is used with a random nonce throughout the rest of the communication.

A socket can be utilized directly without a secure handshake by calling CubeSocket's connect method.  The key must be known on either end.

Supports binary data

# Prerequisites
pycube256

# Client Example

key = "Test"  
sock = CubeSocket(key)  
sock.connect("localhost", 99)  
sock.cubesend("Test")  
sock.close()  

# Server Example

host = "localhost"  
sock = CubeSocket("Test")  
sock.bind(host, 99)  
sock.listen(1)  
client, addr = sock.accept()  
cubesock = CubeSocket(client, sock.session_key)  
test = cubesock.cubesock.recv(32)  
print test  
c.close()  
sock.close()  

# CubeWrap Example

cubesock = CubeSocket(sock, key)  
test = cubesock.sock.recv(32)  

# UDP client example

from CubeSocket256 import CubeSocket  

host = "localhost"  
port = 1666  

socket = CubeSocket("NEVER", protocol="UDP")  
socket.sendto("HELLO", host, port)  

# UDP Server example

from CubeSocket256 import CubeSocket

host = "localhost"  
port = 1666  

socket = CubeSocket("NEVER", protocol="UDP")  
socket.bind(host, port)  
while True:  
    data = socket.cuberecvfrom(1024)  
    print data  
