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

def send_request(host, port, request, binary_data=None):
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.connect((host, port))
        s.sendall(request.encode())
        if binary_data:
            s.sendall(binary_data)
        response = s.recv(4096)
    return response

def upload_file(host, port, filename):
    with open(filename, 'rb') as file:
        file_data = file.read()
        content_length = len(file_data)
        request = (
            f"POST /upload HTTP/1.1\r\n"
            f"Host: {host}\r\n"
            f"Content-Length: {content_length}\r\n\r\n"
        )
        # Send the request with binary data
        response = send_request(host, port, request, binary_data=file_data)
    return response.decode()

def download_file(host, port, filename):
    request = f"GET /{filename} HTTP/1.1\r\nHost: {host}\r\n\r\n"
    response = send_request(host, port, request)
    # Split headers and file content
    header, file_content = response.split(b'\r\n\r\n', 1)
    with open(filename, 'wb') as file:
        file.write(file_content)

if __name__ == "__main__":
    host = 'example.com'  # Replace with actual server IP or domain
    port = 80             # Replace with actual port if different

    # Upload file
    upload_response = upload_file(host, port, r"C:\Users\admin\Desktop\computer_networks\exp5a\example.txt")
    print("Upload response:", upload_response)

    # Download file
    download_file(host, port, 'example.txt')
    print("File downloaded successfully.")
```

## OUTPUT

![image](https://github.com/user-attachments/assets/f1cfce13-e0ed-49b0-92b4-55fcf8f62fd7)


## Result
Thus the socket for HTTP for web page upload and download created and Executed
