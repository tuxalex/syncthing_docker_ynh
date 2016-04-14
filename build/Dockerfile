# VERSION 0.1
# DESCRIPTION:    syncthing server conatiner
# TO_BUILD:       docker build -rm -t syncthing .
# TO_RUN:         docker run -d --name=syncthing -i -t -p 8384:8384 -p 22000:22000 -p 21027:21027/udp -v /PATHDATA/:/home/syncthing/.config/ -v /PATHCONFIG/:/home/syncthing/data IMAGENAME

FROM ubuntu-debootstrap:14.04
MAINTAINER : Alexan Andrieux <alexan.andrieux@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN useradd -m syncthing
RUN mkdir -p "/home/syncthing/.config"
RUN mkdir -p "/home/syncthing/.config/syncthing"
RUN mkdir -p "/home/syncthing/Sync"
RUN apt-get update && apt-get install -qy --force-yes ca-certificates curl

RUN set -x \
    && curl -s https://syncthing.net/release-key.txt | apt-key add - \
    && echo "deb http://apt.syncthing.net/ syncthing release" | tee /etc/apt/sources.list.d/syncthing.list \
    && apt-get update && apt-get install -qy --force-yes syncthing \
    #&& tarball="syncthing-linux-amd64-v${SYNCTHING_VERSION}.tar.gz" \
    #&& curl -fSL "https://github.com/syncthing/syncthing/releases/download/v${SYNCTHING_VERSION}/"{"$tarball",sha1sum.txt.asc} -O \
    #&& tar -xvf "$tarball" --strip-components=1 "$(basename "$tarball" .tar.gz)"/syncthing \
    #&& mv syncthing /sbin/syncthing \
    #&& rm "syncthing-linux-amd64-v${SYNCTHING_VERSION}.tar.gz" \
    && ln -s /home/syncthing/Sync /home/syncthing/data 

RUN chown -R syncthing:syncthing /home/syncthing/
RUN find /home/syncthing/ -type f | while read LINE; do chmod 640 "$LINE" ; done
RUN find /home/syncthing/ -type d | while read LINE; do chmod 750 "$LINE" ; done

WORKDIR /home/syncthing/
USER syncthing

EXPOSE 8384
EXPOSE 22000/tcp
EXPOSE 21027/udp 

VOLUME ["/home/syncthing/.config/", "/home/syncthing/data/"]

ENTRYPOINT ["syncthing"]
