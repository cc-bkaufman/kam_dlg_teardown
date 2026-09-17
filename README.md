## Testing dialog state lifetime
Checking the manner in which a dialog is destroyed


## Running
My preference is to use multiple `screen` instances (you may prefer `tmux`). I
create a few screens from the root of this project with the following:

- screen 0: Use this to start/stop docker-compose and observe logs.  After
creating this screen run:
    ```
    docker compose up
    docker logs -f kamailio
    ```

- screen 1: I use this to execute commands in the `uac` container.  The working
directory for the container is `/data` and this directory contains a scripts
that will excute a `sipexer` command to send messagse to `kamailio`.

- screen 2: I use this to run `sngrep` on the `kamailio` container. To do this,
after starting the screen run:
    ```
    docker compose exec kamailio sngrep
    ```


Once all containers are running, and the screens are created, on screen 1 (in
the `uac` container), run `./invite_and_bye.sh`, and you'll see that the
concurrent call count increases by 1 at the `INVITE`, stays at 1 during the
`ACK`, and drops back to 0 on the `BYE`, even thought the BYE can't be
delivered.  You can continue to run `./invite_and_bye.sh`, and this pattern
persists.

Conversely, run the `invite_only.sh` script, which does not send a `BYE`, and
the concurrent call counter will climb with each invocation.

