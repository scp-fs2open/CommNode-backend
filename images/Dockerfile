FROM ubuntu:18.04

ARG fso_version

RUN apt-get update && apt-get install -y libopenal1 libsdl2-2.0-0 libfreetype6 unzip

# If the package is available locally then the COPY below would also work
ADD https://github.com/scp-fs2open/fs2open.github.com/releases/download/release_${fso_version}/fs2_open_${fso_version}-builds-Linux.tar.gz /build/builds.tar.gz
#COPY fs2_open_${fso_version}-builds-Linux.tar.gz /build/builds.tar.gz

RUN cd /build && tar -xzvf builds.tar.gz
RUN cd /build && ./fs2_open_${fso_version}_x64-FASTDBG.AppImage --appimage-extract
RUN mkdir /fso-bin && cd /fso-bin && cp -r /build/squashfs-root/. .

ADD https://github.com/scp-fs2open/fs2open_webui/archive/master.zip /build/webui.zip
RUN unzip /build/webui.zip -d /build/fso-webui && cp -r /build/fso-webui/fs2open_webui-master/. /fso-webui

RUN rm -r /build

ENV XDG_DATA_HOME=/fso-config
COPY fs2_open.ini /fso-config/HardLightProductions/FreeSpaceOpen/
COPY multi.cfg /fso-config/HardLightProductions/FreeSpaceOpen/data/

EXPOSE 8080 7808/udp

VOLUME ["/fso"]
WORKDIR /fso
ENTRYPOINT ["/fso-bin/AppRun", "-nosound", "-standalone", "-noninteractive", "-port", "7808"]
