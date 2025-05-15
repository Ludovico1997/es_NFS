# Accesso a Storage NFS in Container tramite Bind Mount

In questo progetto rendiamo accessibile uno **storage NFS persistente**, ospitato su una **VM server**, a un **container in esecuzione su una VM client**.

## Architettura


## Metodo: Bind Mount

Utilizziamo il metodo del **Bind Mount**, che prevede i seguenti passaggi:

**Mount NFS nella VM client**:
   Montiamo manualmente o via `/etc/fstab` la directory NFS condivisa dal server.
   ```bash
   sudo mount -t nfs 192.168.168.111:/mnt/nfs_share /mnt/nfs_mount
