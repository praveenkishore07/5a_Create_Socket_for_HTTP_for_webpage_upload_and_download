# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm

1.Start the program.
<BR>
2.Get the frame size from the user
<BR>
3.To create the frame based on the user request.
<BR>
4.To send frames to server from the client side.
<BR>
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
<BR>
6.Stop the program
<BR>
## Program 
```
Developed by: A PRAVEEN KISHORE
Register no.: 212225220074
```
## Server -
```
import socket

s = socket.socket()
s.bind(("localhost",8080))
s.listen(1)

print("Server running...")

while True:
    c,addr = s.accept()
    
    request = c.recv(1024).decode()
    print("Request received")

    if "GET" in request:
        f = open("index.html","r")
        data = f.read()
        f.close()

        response = "HTTP/1.1 200 OK\n\n" + data
        c.send(response.encode())

    elif "POST" in request:
        data = request.split("\n\n")[1]

        f = open("index.html","a")
        f.write(data)
        f.close()

        c.send("HTTP/1.1 200 OK\n\nFile Uploaded".encode())

    c.close()
```
## Client -
```
import socket

s = socket.socket()
s.connect(("localhost",8080))

ch = input("1-Download 2-Upload : ")

# Download webpage
if ch == "1":
    req = "GET / HTTP/1.1\nHost: localhost\n\n"
    s.send(req.encode())

    data = s.recv(4096)
    print(data.decode())

# Upload file
else:
    msg = input("Enter data to upload: ")

    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
    s.send(req.encode())

    data = s.recv(1024)
    print(data.decode())

s.close()
```

## OUTPUT
## Download---
<img width="1302" height="227" alt="download" src="https://github.com/user-attachments/assets/c8abf449-b2e0-4028-a0cf-db5e6ed126ca" />

## Upload---
<img width="1322" height="211" alt="upload" src="https://github.com/user-attachments/assets/648299c3-ba51-46eb-861b-6cd35b0cb213" />

## After uploading....

<img width="400" height="191" alt="updated " src="https://github.com/user-attachments/assets/c8e3a631-5913-4476-8829-587fd0e06d8b" />



## Result
Thus the socket for HTTP for web page upload and download created and Executed
