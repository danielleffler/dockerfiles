FROM alpine:latest

LABEL description="terraria-server" \
      maintainer="Khoa Nguyen <khoa.tan.nguyen.96@gmail.com>"

ENV TERRARIA_VER=1353
ENV SERVER_ROOT=/opt/terraria
ENV LOG_ROOT=/var/log/terraria

# http://terraria.org/system/dedicated_servers/archives/000/000/032/original/terraria-server-1353.zip?1515098333
RUN apk add --no-cache \
  wget \
  zip \
  && mkdir -p ${SERVER_ROOT}/ \
  && mkdir -p ${LOG_ROOT} \
  && wget -q http://terraria.org/system/dedicated_servers/archives/000/000/032/original/terraria-server-${TERRARIA_VER}.zip -O /tmp/terraria.zip \
  && unzip /tmp/terraria.zip ${TERRARIA_VER}/Linux/* -d ${SERVER_ROOT} \
  && rm -rf /tmp/* \
  && cd ${SERVER_ROOT}/${TERRARIA_VER}/Linux \
  && chmod a+rw * \
  && chmod a+x TerrariaServer*

VOLUME ["/world"]
EXPOSE 7777

WORKDIR ${SERVER_ROOT}/${TERRARIA_VER}/Linux
COPY server.conf .
COPY entrypoint.sh /usr/local/bin/entrypoint.sh

ENTRYPOINT [ "/usr/local/bin/entrypoint.sh" ]