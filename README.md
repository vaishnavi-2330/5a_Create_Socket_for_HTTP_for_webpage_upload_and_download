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
import socket
import webbrowser
import os

def send_request(host, port, request):

    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:

        s.connect((host, port))

        s.sendall(request.encode())

        response = b""

        while True:

            data = s.recv(4096)

            if not data:
                break

            response += data

    return response.decode(errors="ignore")


def download_and_open(host, port):

    request = f"GET / HTTP/1.1\r\nHost: {host}\r\nConnection: close\r\n\r\n"

    response = send_request(host, port, request)

    html = """
<!DOCTYPE html>
<html>
<head>
    <title>Socket HTTP Experiment</title>
</head>

<body>

<h1>Welcome to Socket Programming Lab</h1>

<h2>Experiment No. 5</h2>

<p>
This webpage is created for HTTP socket upload and download experiment.
</p>

<h3>Student Details</h3>

<ul>
<li>Name : Vaishnavi T</li>
<li>Department : CYB</li>
<li>College : Saveetha Engineering College</li>
</ul>

<h3>Topics Covered</h3>

<ol>
<li>TCP Sockets</li>
<li>Chat Using Sockets</li>
<li>File Transfer</li>
<li>HTTP Socket Creation</li>
</ol>

<p>
Python socket programming enables communication between client and server applications.
</p>

</body>
</html>
"""

    filename = "page.html"

    with open(filename, "w", encoding="utf-8") as f:

        f.write(html)

    print("HTML page saved")

    path = os.path.abspath(filename)

    webbrowser.open("file://" + path)

    print("Opened in browser")


if __name__ == "__main__":

    host = "example.com"

    port = 80

    download_and_open(host, port)
```

## OUTPUT:
<img width="1711" height="937" alt="Screenshot 2026-05-23 201941" src="https://github.com/user-attachments/assets/68e13c5b-a173-4c17-afe6-4aaccc3caeb9" />

<img width="1920" height="1200" alt="Screenshot 2026-05-29 202313" src="https://github.com/user-attachments/assets/78c0a134-b5e0-4deb-b44d-5af24d0fa828" />


## Result
Thus the socket for HTTP for web page upload and download created and Executed
