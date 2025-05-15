# Montaggio Diretto di Share NFS all'interno di un Container Docker

Questa configurazione permette a un container Docker di **montare direttamente** una share NFS al suo interno, senza passare da un volume Docker o bind mount del sistema host.

## Requisiti

- Docker deve essere eseguito su una macchina Linux.
- Il container deve essere avviato con i flag `--privileged` e `--cap-add=SYS_ADMIN`.
- Il pacchetto `nfs-common` deve essere installato **all'interno del container**.

---

## Esecuzione del container

Avvia un container interattivo con i privilegi necessari per montare la share NFS:

```bash
sudo docker run -it --rm \
  --cap-add=SYS_ADMIN \
  --privileged \
  ubuntu bash

