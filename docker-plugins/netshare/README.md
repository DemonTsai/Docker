# Docker Volume Plugin Image: docker-volume-netshare
  A docker volume plugin for NFS, AWS EFS & Samba/CIFS. Mount NFS v3/4, AWS EFS or CIFS inside your docker containers. This is a docker volume plugin which enables these volume types to be directly mounted within a container. Source: **_[ContainX/docker-volume-netshare](https://github.com/ContainX/docker-volume-netshare)_**

- - -

## Prerequisites
  * Create directories for plugin:
    ```
    $ sudo mkdir -p /run/docker/plugins
    $ sudo mkdir -p /var/lib/docker-volumes/netshare
    ```

  * Mount as a rshared directory:
    ```
    $ sudo mount --bind /var/lib/docker-volumes/netshare /var/lib/docker-volumes/netshare
    $ sudo mount --make-rshared /var/lib/docker-volumes/netshare
    ```

- - -

## Usage
  * Run plugin:

    ```
    $ docker run -d --name netshare -h netshare --restart=always --privileged -v /run/docker/plugins:/run/docker/plugins -v /var/lib/docker-volumes/netshare:/var/lib/docker-volumes/netshare:rshared demontsai/netshare:0.31-alpine
    ```

  * Create a volume of nfs type:
    ```
    $ docker volume create -d nfs --name nfs-dir -o share=YOUR_NFS_SERVER:/your_share_dir
    ```

  * Run your container mount nfs volume:
    ```
    $ docker run -itd --name my_container -v nfs-dir:/path_in_your_container ubuntu:14.04 bash
    ```
