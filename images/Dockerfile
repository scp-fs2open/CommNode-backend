FROM ubuntu:18.04

ARG fso_version

RUN apt-get update && apt-get install -y libopenal1 libsdl2-2.0-0 libfreetype6

# If the package is available locally then the COPY below would also work
ADD https://github.com/scp-fs2open/fs2open.github.com/releases/download/release_${fso_version}/fs2_open_${fso_version}-builds-Linux.tar.gz /builds/builds.tar.gz
#COPY fs2_open_${fso_version}-builds-Linux.tar.gz /builds/builds.tar.gz

RUN cd /builds && tar -xzvf builds.tar.gz

RUN cd /builds && ./fs2_open_${fso_version}_x64.AppImage --appimage-extract

RUN mkdir /fso-bin && cd /fso-bin && cp -r /builds/squashfs-root/. . && rm -r /builds

VOLUME ["/fso"]
WORKDIR /fso
ENTRYPOINT ["/fso-bin/AppRun", "-nosound", "-standalone", "-portable_mode", "-noninteractive"]
