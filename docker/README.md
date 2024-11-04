## Cheatsheet

## Delete everything
```sh
# https://stackoverflow.com/questions/44785585/how-can-i-delete-all-local-docker-images
docker system prune -a --volumes
```
> WARNING! This will remove:
    - all stopped containers
    - all networks not used by at least one container
    - all volumes not used by at least one container
    - all images without at least one container associated to them
    - all build cache

## Relocating the Docker root directory
https://www.ibm.com/docs/en/z-logdata-analytics/5.1.0?topic=software-relocating-docker-root-directory
```sh
sudo systemctl stop docker
sudo systemctl stop docker.socket
sudo systemctl stop containerd


sudo mkdir -p /new_dir_structure

sudo mv /var/lib/docker /new_dir_structure

sudo nano /etc/docker/daemon.json
sudo systemctl start docker
docker info -f '{{ .DockerRootDir}}'
```
```sh
# /etc/docker/daemon.json
{
  "data-root": "/new_dir_structure/docker"
}
```
https://stackoverflow.com/a/49743270/12603110
```
sudo systemctl stop docker
sudo mv /var/lib/docker/ /path/to/new/docker/
sudo ln -s /path/to/new/docker/ /var/lib/docker
sudo systemctl start docker
```