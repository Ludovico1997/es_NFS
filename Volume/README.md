# Condivisione di Storage NFS in Container tramite Volume Docker

Questa configurazione consente a un container Docker in esecuzione su una **VM client** di accedere a uno **storage NFS persistente**, esposto da una **VM server**, utilizzando un **volume Docker** con driver `local`.
Questo metodo è utile, ad esempio, se vogliamo utilizzare lo stesso volume in più Container 

### Installazione tramite Docker Compose

```yaml 
    services:
    app:
        image: my-container-image
        volumes:
        - my_nfs_volume:/app/nfs_share

    volumes:
    my_nfs_volume:
        driver: local
        driver_opts:
        type: "nfs"
        o: "addr=192.168.168.111,rw"
        device: ":/mnt/nfs_share"
