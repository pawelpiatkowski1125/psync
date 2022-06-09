### Synchronize directories between a remote machine and a pod

A typical use case for this tool is copying a large number of files
from a remote machine (accessible over SSH) to a persistent volume
attached to a Kubernetes pod.

To use `psync`, follow these steps:

1. Optionally build a Docker image with `rsync` compiled in:
    ```docker build -t sync-image .```
   Note: this is only for your convenience; any off-the-shelf
   image can be used instead.
2. Register an auxiliary pod on the Kubernetes cluster:
    ```kubectl apply -f sync-pod.yaml```
   Remember to change the PVC name beforehand!
3. Make sure your connection to the remote machine works.
4. Check the paths.
5. Run:
    ```psync [-p port] machine:/source/path sync-pod:/dest/path```
   where `port` is an optional custom SSH port.

Mind the trailing slashes (or lack thereof) - they are important!

If the synchronization fails, simply rerun it, setting the `-t` parameter.
(Copy the temporary directory path from the script's output.)

Disclaimer:
`krsync` is copyright by Karl Bunch (https://serverfault.com/a/887402)
