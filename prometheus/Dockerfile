FROM arm32v6/alpine

WORKDIR /root
RUN apk add --update bash \
libarchive-tools \
wget

RUN mkdir -p /usr/share/prometheus && \
mkdir -p /etc/prometheus && \
wget https://github.com/prometheus/prometheus/releases/download/v2.6.0/prometheus-2.6.0.linux-armv6.tar.gz -O /root/prometheus.tar.gz && \
bsdtar -xvf prometheus.tar.gz -C ./ --strip-components=1 && \
rm prometheus.tar.gz && \
mv prometheus /bin/prometheus && \
mv promtool /bin/promtool && \
mv prometheus.yml /etc/prometheus/prometheus.yml && \
cp -r console_libraries/ /usr/share/prometheus/console_libraries/ && \
cp -r consoles/ /usr/share/prometheus/consoles/ && \
rm LICENSE && \
rm NOTICE && \
rm -r console_libraries && \
rm -r consoles

EXPOSE     9090
VOLUME     [ "/etc/prometheus" ]
VOLUME     [ "/prometheus" ]
WORKDIR    /prometheus
ENTRYPOINT [ "/bin/prometheus" ]
CMD        [ "-config.file=/etc/prometheus/prometheus.yml", \
             "-storage.local.path=/prometheus", \
             "-web.console.libraries=/usr/share/prometheus/console_libraries", \
             "-web.console.templates=/usr/share/prometheus/consoles" ]
