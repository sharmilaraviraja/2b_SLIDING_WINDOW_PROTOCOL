# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
# Client.py
```
import socket

# Create socket
client = socket.socket() 
client.connect(('localhost', 8000))

while True:
    # Receive data from server
    data = client.recv(1024).decode()
    
    if not data:
        break
    
    print("Received:", data)

    # Send acknowledgment
    client.send("Acknowledgement received from the server".encode())

# Close connection
client.close()
```
# Server.py
```
import socket

# Create socket
server = socket.socket()
server.bind(('localhost', 8000))
server.listen(5)

print("Server waiting for connection...")
c, addr = server.accept()
print("Connected to:", addr)

# Input values
size = int(input("Enter number of frames to send: "))
frames = list(range(size))

window_size = int(input("Enter Window Size: "))

start = 0
i = 0

while i < len(frames):
    start = i + window_size
    window = frames[i:start]

    # Send window frames
    c.send(str(window).encode())
    print("Sent:", window)

    # Receive acknowledgment
    ack = c.recv(1024).decode()
    if ack:
        print("Received ACK:", ack)
        i += window_size

# Close connection
c.close()
server.close()
```
## OUPUT
<img width="1919" height="1140" alt="image" src="https://github.com/user-attachments/assets/d5731a67-a8f4-4dc7-bce9-6f0a037b1ead" />
<img width="1483" height="879" alt="image" src="https://github.com/user-attachments/assets/06f5bcfb-bb1b-468f-b6a0-06209acf614e" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
