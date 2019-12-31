FROM postgres:11
MAINTAINER Mike Dillon <mike@appropriate.io>

ENV POSTGIS_MAJOR 3.0
ENV POSTGIS_VERSION 3.0.0+dfsg-2~exp1.pgdg18.04+1_amd64.deb

RUN apt-get update \
      && apt-cache showpkg postgresql-$PG_MAJOR-postgis-$POSTGIS_MAJOR \
      && apt-get install -y --no-install-recommends \
           postgresql-$PG_MAJOR-postgis-$POSTGIS_MAJOR=$POSTGIS_VERSION \
           postgresql-$PG_MAJOR-postgis-$POSTGIS_MAJOR-scripts=$POSTGIS_VERSION \
           postgis=$POSTGIS_VERSION \
      && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y aptitude  \
      && aptitude update \
      && aptitude install -y nano axel wput screen p7zip-full osmium-tool \
      htop vnstat gdal-bin


RUN mkdir -p /docker-entrypoint-initdb.d
COPY ./initdb-postgis.sh /docker-entrypoint-initdb.d/postgis.sh
COPY ./update-postgis.sh /usr/local/bin
