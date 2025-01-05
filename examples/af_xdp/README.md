# TRex Example: AF_XDP PMD in Container

## Get Started

1.  Start TRex server for stateless mode.

    ```bash
    make stl.server
    ```

2.  Connect to the TRex server with console.

    ```bash
    make stl.console
    ```

3.  Start UDP traffic at 10 Gbps on all ports

    ```bash
    trex>start -f stl/udp_1pkt_simple.py -m 10gbpsl1
    ```

    Note: It only achieves about 2.8 Gbps L1 throughput on my computer.

4.  Show dynamic statistics.

    ```bash
    trex>tui
    ```

    You can then exit the statistics interface by

    ```bash
    tui>exit
    ```

5.  After finishing, stop the traffic on all ports; exit the console; and then
    stop the TRex server.

    ```bash
    trex>stop -a
    trex>exit
    make stl.server.down
    ```
