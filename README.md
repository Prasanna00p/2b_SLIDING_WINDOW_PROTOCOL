# EX 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM:
Implementation of sliding window protocol
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM


Client.py

```
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
c, addr = s.accept()

size = int(input("Enter number of frames to send: "))
l = list(range(size))
s_win = int(input("Enter Window Size: "))

st = 0
i = 0

while True:
    while i < len(l):
        st += s_win
        c.send(str(l[i:st]).encode())
        ack = c.recv(1024).decode()
        if ack == "ack":
            print("Acknowledgment received:", ack)
            i += s_win


```
Server.py

```
import socket
import time

s = socket.socket()
s.connect(('localhost', 8000))

while True:
    msg = s.recv(1024).decode()
    print("Received:", msg)
    time.sleep(0.5)  # Prevents immediate loop, optional
    s.send("ack".encode())
```

## OUPUT

![Screenshot 2025-04-12 105945](https://github.com/user-attachments/assets/8b83008a-0327-4cc1-8e5f-ef3d65f00db3)


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
