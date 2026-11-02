# ShellSpace

A simple terminal-based chat room built with Python. ShellSpace lets one
user host a chat room and share it with others through an ngrok TCP
tunnel. Participants can join from another computer using the host's
public address, a room password, and a username.

## Features

-   **Host a chat room** from the command-line menu.
-   **Join an existing room** using the host's ngrok address.
-   **Password-protected entry** so only people with the room password
    can join.
-   **Multiple participants** can chat in the same room.
-   **Colored messages** to make usernames easier to distinguish.
-   **Host moderation** with a command to kick a participant.
-   **Chat history logging** saved locally in `log/history.txt`.
-   **ngrok TCP tunneling** so participants can connect over the
    internet.

## Requirements

-   Python 3
-   pip
-   An [ngrok](https://ngrok.com/) account and authentication token
-   Internet access

## Installation

1.  Clone the repository:

    ``` bash
    git clone https://github.com/linuxmnster/ShellSpace_Py.git
    ```

2.  Open the project folder:

    ``` bash
    cd ShellSpace_Py
    ```

3.  Install the Python dependencies:

    ``` bash
    pip install -r requirements.txt
    ```

## Configure ngrok

ShellSpace uses ngrok to expose the host's local chat server.

1.  Create or sign in to your ngrok account: https://ngrok.com/

2.  Copy your ngrok authentication token from the ngrok dashboard.

3.  Run ShellSpace:

    ``` bash
    python main.py
    ```

4.  Choose **`3 - Set ngrok Token`** and paste your token when prompted.

    The application saves the token in `core/token.txt`. The ngrok
    helper reads this file when a room is hosted.

> **Keep your ngrok token private.** Do not commit `core/token.txt` or
> share it publicly. If it has already been uploaded, revoke or rotate
> it in your ngrok account.

## Run the Application

From the project directory, start the program:

``` bash
python main.py
```

The menu provides these options:

  Option   Action
  -------- ------------------------------------
  `1`      Host a room
  `2`      Join a room
  `3`      Set the ngrok authentication token
  `4`      Clear the terminal
  `0`      Exit ShellSpace

### Host a room

1.  Select **`1 - Host a Room`**.
2.  Enter a password for the room.
3.  Wait for ShellSpace to start the ngrok TCP tunnel.
4.  Share the displayed `hostname:port` address and room password with
    participants.
5.  Keep the host application running while people are connected.

Host commands:

  Command            Action
  ------------------ -------------------------------------------
  `/kick username`   Remove the participant with that username
  `/exit`            Shut down the chat room

### Join a room

1.  Start ShellSpace on your computer.
2.  Select **`2 - Join a Room`**.
3.  Enter the `hostname:port` address shared by the host.
4.  Enter the room password.
5.  Choose a username and start chatting.

Use `/leave` to leave the chat.

## Project Structure

``` text
ShellSpace_Py/
│
├── core/
│   ├── client.py          # Connects to a hosted chat room
│   ├── server.py          # Hosts the room and manages participants
│   └── ngrok_handle.py    # Starts the ngrok TCP tunnel
│
├── config.py              # Chat server port configuration
├── main.py                # Application entry point and menu
├── requirements.txt       # Python dependencies
└── README.md              # Project documentation
```

The application creates `core/token.txt` when you save your ngrok token
and creates `log/history.txt` when you host a room.

## Configuration

The default chat server port is set in `config.py`:

``` python
PORT = 9090
```

Change this value if you need to use a different port, making sure it is
available on the host machine.

## Dependencies

The project uses the following Python packages:

-   **pyngrok** -- creates the ngrok TCP tunnel.
-   **colorama** -- adds colored terminal output.
-   **pyfiglet** -- displays the ShellSpace banner.

Install all dependencies with:

``` bash
pip install -r requirements.txt
```

## Notes & Safety

-   The host must keep ShellSpace running for the room to remain
    available.
-   Participants need the correct ngrok address and room password.
-   Do not share your ngrok authentication token.
-   The current project uses a basic socket-based chat implementation.
    Do not use it to exchange passwords, private information, or other
    sensitive data.
-   Chat history is stored locally by the host in `log/history.txt`.

## Contributing

Contributions and suggestions are welcome. You can fork the repository,
make your changes, and submit a pull request.

## License

No license is currently specified for this repository. Check with the
repository owner before reusing or distributing the code.

------------------------------------------------------------------------

Made with Python.
