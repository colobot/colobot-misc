This is the Docker image for use on our Jenkins server

It contains GCC8 so that we can catch new warnings early and MXE

Get it from https://hub.docker.com/r/krzysh/colobot-build/

If you want to build the package manually (warning: will build all of the MXE packages required by Colobot) just type `docker build -t colobot-build .`

To download the package and enter shell inside the container, mounting the current working directory as /home: `sudo docker run -v \`pwd\`:/home -it krzysh/colobot-build bash`

To build Colobot using both GCC8 and MXE:
```sh
git clone -b dev https://github.com/colobot/colobot.git; cd colobot
docker run -v `pwd`:/home -it krzysh/colobot-build bash -c "mkdir -p /home/build; cd /home/build; cmake ..; make -j9"
docker run -v `pwd`:/home -it krzysh/colobot-build bash -c "mkdir -p /home/build-mxe; cd /home/build-mxe; /opt/mxe/usr/bin/i686-w64-mingw32.static-cmake ..; make -j9"
```
