# Java Chat Application

A simple multi-client chat application built with Java socket programming. This project demonstrates basic networking concepts including client-server architecture, multithreading, and real-time message broadcasting.

## Features

- **Multi-Client Support**: Multiple users can connect and chat simultaneously
- **Real-Time Messaging**: Messages are broadcast instantly to all connected clients
- **Server Admin Controls**: Server can send messages to all clients
- **Username System**: Each client identifies themselves with a username
- **Thread-Safe**: Uses `CopyOnWriteArrayList` for safe concurrent access
- **Console-Based**: Simple command-line interface for both server and clients

## Components

### Server.java
The central server that:
- Listens for incoming client connections on port 12346
- Manages all connected clients
- Broadcasts messages from any client to all other clients
- Allows server admin to send messages to all clients
- Handles client disconnections gracefully

### Client.java
The client application that:
- Connects to the server
- Allows users to set their username
- Sends messages typed in the console
- Receives and displays messages from other users in real-time

### Client2.java
An identical copy of `Client.java` for testing multiple connections (can be used to simulate a second user)

## Requirements

- Java Development Kit (JDK) 8 or higher
- No external dependencies required

## Installation

1. Save the three files:
   - `Server.java`
   - `Client.java`
   - `Client2.java`

2. Compile all files:
```bash
   javac Server.java Client.java Client2.java
```

## Usage

### Starting the Server

1. Run the server first:
```bash
   java main.Server
```
2. You should see: `Server is running and waiting for connections...`
3. The server can type messages that will be broadcast to all clients

### Connecting Clients

1. In separate terminal windows, run the client(s):
```bash
   java main.Client
```
   Or for a second client:
```bash
   java main.Client2
```

2. When prompted, enter your username
3. Start typing messages to chat with other connected users

### Example Session

**Server Terminal:**
```
Server is running and waiting for connections...
New client connected: Socket[addr=/127.0.0.1,port=54321,localport=12346]
User Alice connected.
New client connected: Socket[addr=/127.0.0.1,port=54322,localport=12346]
User Bob connected.
[Alice]: Hello everyone!
[Bob]: Hi Alice!
```

**Client 1 Terminal (Alice):**
```
Connected to the chat server!
Enter your username:
Alice
Welcome to the chat, Alice!
Type Your Message
Hello everyone!
[Bob]: Hi Alice!
[Server]: Welcome to the chat room!
```

**Client 2 Terminal (Bob):**
```
Connected to the chat server!
Enter your username:
Bob
Welcome to the chat, Bob!
Type Your Message
[Alice]: Hello everyone!
Hi Alice!
[Server]: Welcome to the chat room!
```

## Configuration

To change the server address or port, modify these constants in the code:

**In Server.java:**
```java
private static final int PORT = 12346;
```

**In Client.java and Client2.java:**
```java
private static final String SERVER_ADDRESS = "localhost";
private static final int SERVER_PORT = 12346;
```

## How It Works

1. **Server Setup**: The server creates a `ServerSocket` that listens on port 12346
2. **Client Connection**: When a client connects, the server creates a new `ClientHandler` thread
3. **Username Registration**: Each client is prompted to enter a username
4. **Message Broadcasting**: When any client sends a message, it's broadcast to all other connected clients
5. **Multithreading**: Each client runs in its own thread, allowing simultaneous communication

## Architecture
```
Server (Port 12346)
    ├── ClientHandler Thread 1 (Alice)
    ├── ClientHandler Thread 2 (Bob)
    ├── ClientHandler Thread 3 (Charlie)
    └── Server Admin Input Thread
```

## Limitations & Known Issues

- No message encryption or security
- No persistent message history
- No private messaging between users
- No authentication system
- Server address is hardcoded to localhost (for local testing only)
- No GUI (command-line only)

## Potential Improvements

- Add GUI with JavaFX or Swing
- Implement private messaging
- Add message timestamps
- Create user authentication
- Add message encryption
- Store chat history
- Support file transfers
- Add user lists showing who's online
- Implement chat rooms
- Add emoji support

## Testing Multiple Clients

To test with multiple clients on the same machine:
1. Run `Server.java` once
2. Run `Client.java` in one terminal
3. Run `Client2.java` (or another instance of `Client.java`) in another terminal
4. Type messages in either client to see them broadcast

## Troubleshooting

**"Connection refused" error:**
- Make sure the server is running before starting clients
- Check that the port 12346 is not already in use

**Messages not appearing:**
- Verify all clients are connected to the same server
- Check for firewall blocking the port

**Server crashes:**
- Ensure proper exception handling
- Check that port 12346 is available

## License

This is an educational project. Feel free to use and modify as needed.

## Author

Created by BinaM122
