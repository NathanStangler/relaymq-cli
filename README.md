# relaymq-cli

Command line client for interacting with RelayMQ message brokers.

## Build

Requires GCC 14+ and CMake 3.25+:

```bash
cmake -B build -DCMAKE_BUILD_TYPE=Release
cmake --build build -j
```

## Usage

```bash
# Publish a message
./build/relay-cli pub <subject> <payload> [host:port] [--token <tok>]

# Subscribe and listen for messages
./build/relay-cli sub <subject> [host:port] [--token <tok>]

# Request-reply RPC
./build/relay-cli req <subject> <payload> [host:port] [--token <tok>] [--timeout <ms>]

# Ping broker and measure latency
./build/relay-cli ping [host:port] [--token <tok>] [--timeout <ms>]
```

Defaults: `host = 127.0.0.1`, `port = 9000`.
