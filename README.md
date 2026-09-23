# ECE312 — Computer Networks

Networking and communication coursework from Rose-Hulman Institute of Technology. The collection includes C socket programs, Python echo examples, a chat client/server pair, process/thread server experiments, and a UDP packet-format exercise.

Original project title: **ECE312_NetworkingCommunication**.

## Project guide

| Directory | Contents |
| --- | --- |
| [project1 - sockets/](project1%20-%20sockets/) | TCP socket clients and servers, chat programs, fork/thread experiments, and Python echo examples |
| [project2/](project2/) | UDP client protocol exercise, uppercase UDP server example, header definitions, and original course data/log files |

These are separate exercises. There is no single application that starts every program at once.

## Requirements

- A POSIX socket environment, such as Linux or WSL, for the C programs.
- A C compiler and Make; thread examples use pthreads.
- Python 3 for the Python echo examples; they use the standard library.

The directories contain historical compiled executables. Build from source for your own system rather than assuming those binaries match it.

## Project 1: socket programming

Build the C programs from the repository root:

```sh
make -C "project1 - sockets"
```

The Makefile builds `forkServer`, `ThreadServer`, `socketsClient`, `socketsServer`, `chatServer`, and `chatClient`.

### Basic C client/server example

Run the server and client in separate terminals. Both commands below assume the repository root as the working directory:

```sh
# Terminal 1
"./project1 - sockets/socketsServer" 9000
```

```sh
# Terminal 2
"./project1 - sockets/socketsClient" 127.0.0.1 9000
```

Follow the client's terminal prompt to send a message. Use the same port for both processes. The chat and fork/thread variants are separate experiments; review their source for their own inputs and behavior.

### Python echo example

```sh
# Terminal 1
python3 "project1 - sockets/echo-server.py" 65432
```

```sh
# Terminal 2
python3 "project1 - sockets/echo-client.py" 127.0.0.1 65432
```

The client sends `Hello, world` and prints the returned bytes. The default port is `65432`; the server accepts an optional port argument and the client accepts a host and port. The server implementation binds to all local interfaces.

To remove the C build outputs:

```sh
make -C "project1 - sockets" clean
```

## Project 2: UDP and packet formatting

| File | Role |
| --- | --- |
| [udpClient - example.c](project2/udpClient%20-%20example.c) | Course protocol client, including packet fields, checksums, message requests, and ID requests |
| [pro2Header.h](project2/pro2Header.h) | Server, port, buffer sizes, message types, and protocol constants |
| [udpServer - example.c](project2/udpServer%20-%20example.c) | A separate uppercase-response UDP example on port `9876` |
| [ece312w2122data.csv](project2/ece312w2122data.csv) | Original course reference data |
| [ece312w2122log.txt](project2/ece312w2122log.txt) | Original course log |

The client currently uses port `1874`, as defined in `pro2Header.h`. Its packet protocol and destination differ from the simple UDP server example, so the two should not be treated as an immediately compatible pair.

Before running the client, review its destination and the expected course server. `SERVER` is currently `"localhost"`, but the source passes it to `inet_addr`, which expects a numeric IPv4 address. A local test configuration would therefore need an address such as `127.0.0.1` and a server that implements the matching protocol.

There is no Project 2 Makefile in the current checkout. A modern compiler may also require explicit standard headers: the client uses fixed-width integer types, while the server uses `toupper` and `close`. These setup details are documented here without changing the original source.

## Attribution and development notes

The original [Project 1 README](project1%20-%20sockets/README.md) identifies `socketsClient.c` and `socketsServer.c` as examples from pages 57–58 of the Stallings course text, and the Python echo examples as adapted from [Real Python's socket tutorial](https://realpython.com/python-sockets/#echo-client-and-server). Those notes and source comments remain intact.

The `.vscode/` configurations inside each project include paths from the original development environment and may need local adjustment. The repository is preserved as coursework rather than a production networking library.

Former repository name: `ece312_network_com_project`.
