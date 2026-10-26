# Henon-Based Encryption

A client/server messaging demo that encrypts text with a stream cipher whose keystream comes from the chaotic Hénon map (`a = 1.4`, `b = 0.3`). Both sides start from the same state, so they generate identical keystreams and XOR recovers the plaintext. Built as coursework for Non-Linear Dynamics.

This is a demonstration, not secure cryptography: the key is hard-coded and the keystream is predictable.

## Setup

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Usage

1. Run all cells in `server.ipynb`. It listens on port `65432`.
2. In `client.ipynb`, set `HOST` to the server's IP address. The default, `127.0.0.1`, works when both run on one machine.
3. Run all cells in `client.ipynb`, then enter messages. Type `exit` to quit.

Start the server first, and restart both notebooks before each new session so the keystreams stay in sync. Both machines must be on the same network, and the port must be the same in both notebooks.

## Protocol

Each message is UTF-8 encoded, XORed with the keystream, and sent as a 4-byte big-endian length followed by the ciphertext.
