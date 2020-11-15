# Compile Vib in Docker (of CentOS 7)

The VMWare official vib make tool, i.e. VIB Author, has stopped updating for years. It is based SLES 11 SP2 strictly, no other OS or version works. Thanks for Lamw who make it running in Docker.

## Prepare Docker
1. `Log in CentOS 7 with root`
2. `yum -y install docker`
3. `systemctl start docker`
4. (optional) `systemctl enable docker`
5. `docker pull lamw/vibauthor`

You can test your Docker-vibauthor by :
`docker run --rm -it lamw/vibauthor`
You'll get a new root shell if everything is OK.

## Prepare vib folder tree
1. Get an example from some place, e.g. this repo.
2. Edit descriptor.xml, and put your file into payload folder.
3. Copy the folder to any place to your host, aka CentOS 7.

## Copy folder tree to Docker
1. `docker run --rm -it lamw/vibauthor`
2. `scp -r <usrname>@172.17.0.1:/<vib-folder-on-host> <docker-folder>`, e.g. `scp -r root@172.17.0.1:/build/vib-r8125-example ./vib-8125`

## Compile with vibauthor
1. If you want vib only, just run:
`vibauthor -C -t <your vib folder name>`, e.g. `vibauthor -C -t ./vib-8125 --force` (--force means replace old file)
The vib file will be created in ./vib-8125/ with automatic name.

2. If you want zip bundle, run:
`vibauthor -C -t <your vib folder name> -O <bundle-name>.zip`, e.g. `vibauthor -C -t ./vib-8125 -O r8125-bundle.zip --force`

3. Copy the vib or zip back to your host.

## P.S.
The file or folder name in payload must NOT exceed 8 characters.
