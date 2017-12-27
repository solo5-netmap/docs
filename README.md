# Netmap integration for Solo5

## Technical overview
With this integration, your MirageOS Unikernel program can use 1 TX/RX queue pair provided by Netmap on your host OS. Memory region for the queue pair is shared by both the Unikernel layer(= VM layer) and the Netmap driver layer(= NIC driver) on the host OS layer. So the number of context switches between the VM and host OS can be reduced by taking advantage of a queue-based (like transmission batching) packet handling.

## Memory mapping
4MB memory space for the shared Netmap queue pair is located following the main memory region of your MirageOS Unikernel virtual machine specified by `--mem=`. Therefore, you can set `1020` as the maximum memory size for `--mem=`.

![Memory mapping](/memmap.png)

## Compatibility
You don't need to modify your MirageOS Unikernel code because a Netmap queue handler implemented in the guest kernel layer exports the existing Netif interface for the mirage-tcpip package.
