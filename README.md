# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
To Implement sliding window protocol
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
## Client.py
```
import socket
c = socket.socket()
c.connect(('localhost', 9999))

size = int(input("Enter number of frames to send: "))
l = list(range(size))  
print("Total frames to send:", len(l))
s = int(input("Enter Window Size: "))

i = 0
while True:
    while i < len(l):
        st = i + s
        frames_to_send = l[i:st]  
        print(f"Sending frames: {frames_to_send}")
        c.send(str(frames_to_send).encode())  

        ack = c.recv(1024).decode()  
        if ack:
            print(f"Acknowledgment received: {ack}")
            i += s  

    break
c.close()  
```
## Server.py
```
import socket
s = socket.socket()
s.bind(('localhost', 9999))
s.listen(1)
print("Server listening...")
conn, addr = s.accept()
print(f"Connected to {addr}")

while True:
    frames = conn.recv(1024).decode()
    if not frames:
        break

    print(f"Received frames: {frames}")
    ack_message = f"ACK for frames: {frames}"
    conn.send(ack_message.encode())

conn.close()  
s.close() 
```
## OUPUT
<img width="905" height="128" alt="Screenshot 2025-09-29 162234" src="https://github.com/user-attachments/assets/a67c1feb-9b43-4315-9111-c93002be3b75" />
<img width="888" height="85" alt="Screenshot 2025-09-29 162242" src="https://github.com/user-attachments/assets/40dc692c-0287-49c5-9b99-6722fe9428a7" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
