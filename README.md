Mount share NFS su container


Bind Mount

macchina server:
sudo mkdir -p /mnt/nfs_share
sudo chown nobody:nogroup /mnt/nfs_share
sudo nano /etc/exports
/mnt/nfs_share 192.168.168.0/24(rw,sync,no_subtree_check)
sudo exportfs -a
sudo systemctl restart nfs-kernel-server


macchina client:
sudo mkdir -p /mnt/nfs_mount
sudo mount -t nfs 192.168.168.111:/mnt/nfs_share /mnt/nfs_mount
docker run -it --rm \
  -v /mnt/nfs_mount:/app/nfs_share \
  ubuntu bash

Volume


macchina client:
docker volume create \
  --driver local \
  --opt type=nfs \
  --opt o=addr=192.168.168.111,rw \
  --opt device=:/mnt/nfs_share \
  my_nfs_volume

docker run -it --rm \
  -v my_nfs_volume:/app/nfs_share \
  ubuntu bash


Mount diretto da dentro il container

docker run -it --rm \
  --cap-add=SYS_ADMIN \
  --privileged \
  ubuntu bash

apt update && apt install -y nfs-common
mkdir -p /app/nfs_share
mount -t nfs 192.168.168.111:/mnt/nfs_share /app/nfs_share
