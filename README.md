# 10 Study of socket programming and client-server model Code-blocks
STUDY OF SOCKET PROGRAMMING AND CLIENT SERVER MODEL
# Socket Programming: Client-Server Data Transfer

## 🎯 AIM
To write a Socket program to transfer data between Client and Server.

## 🧰 EQUIPMENTS REQUIRED
- PC with Linux operating system

## 🛠️ PROCEDURE
1. Connect two computers in Wired/Wireless LAN.
2. Ensure both computers are on the same network and can ping each other.
3. Open terminal and type `gedit filename.c` to write the program.
4. Compile using `gcc filename.c`.
5. Execute using `./a.out`.
6. Run the program on both server and client machines.
7. Enter the IP address of the server on the client machine.
8. Enter the data to be transferred and verify its size.

## 💻 PROGRAM

if (WSAStartup(MAKEWORD(2,2), &wsa) != 0) {

    
    printf("WSAStartup failed: %d\n", WSAGetLastError());
    
    return 1;

}



server_sock = socket(AF_INET, SOCK_STREAM, 0);

if (server_sock == INVALID_SOCKET) {

    printf("Could not create socket: %d\n", WSAGetLastError());
    
    WSACleanup(); return 1;

}

server.sin_family = AF_INET;

server.sin_addr.s_addr = INADDR_ANY;

server.sin_port = htons(8888);


if (bind(server_sock, (struct sockaddr *)&server, sizeof(server)) == SOCKET_ERROR) {

    printf("Bind failed: %d\n", WSAGetLastError());
    
    closesocket(server_sock); WSACleanup(); return 1;

}

puts("Bind done. Listening on port 8888...");

listen(server_sock, 3);

c = sizeof(struct sockaddr_in);

client_sock = accept(server_sock, (struct sockaddr *)&client, &c);

if (client_sock == INVALID_SOCKET) {

    printf("Accept failed: %d\n", WSAGetLastError());
    
    closesocket(server_sock); WSACleanup(); return 1;

}

puts("Client connected.");

while ((recv_size = recv(client_sock, client_message, sizeof(client_message)-1, 0)) > 0) {

    client_message[recv_size] = '\0';
    
    send(client_sock, client_message, recv_size, 0);
}


if (recv_size == 0) puts("Client disconnected");

else printf("recv failed: %d\n", WSAGetLastError());

closesocket(client_sock);

closesocket(server_sock);

WSACleanup();

return 0;

OUTPUT:

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e45d5146-828e-4328-b461-2ac30e5ca5be" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/92d3335e-25bd-4ae7-8088-b7d3704f8190" />



## 🎯 RESULT

Thus, a socket program was successfully written to transfer data between client and server, and its performance was studied.
