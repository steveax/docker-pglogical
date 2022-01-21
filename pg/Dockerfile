FROM postgres:11
MAINTAINER Justin Holguin <justin.holguin@puppet.com>

RUN apt-get update && apt-get install -y wget gnupg
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ stretch-pgdg main" > /etc/apt/sources.list.d/pgdg.list \
  && wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | \
       apt-key add - \
  && wget --quiet -O - https://dl.2ndquadrant.com/default/release/get/deb | bash \
  && apt-get install -y postgresql-11-pglogical

# VOLUME /var/lib/postgresql/data # re-volume this so that the config file changes take???

RUN echo "host    replication          postgres                172.18.0.0/16   trust" >> /usr/share/postgresql/11/pg_hba.conf.sample
RUN echo "host    replication          postgres                ::1/128         trust" >> /usr/share/postgresql/11/pg_hba.conf.sample
RUN echo "shared_preload_libraries = 'pglogical'" >> /usr/share/postgresql/postgresql.conf.sample
RUN echo "wal_level = 'logical'" >> /usr/share/postgresql/postgresql.conf.sample
RUN echo "max_wal_senders = 20" >> /usr/share/postgresql/postgresql.conf.sample
RUN echo "max_replication_slots = 20" >> /usr/share/postgresql/postgresql.conf.sample
RUN echo "max_connections = 300" >> /usr/share/postgresql/postgresql.conf.sample

COPY primary.sql /docker-entrypoint-initdb.d/init.sql
