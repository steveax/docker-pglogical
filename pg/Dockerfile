FROM postgres:17-bookworm
MAINTAINER Steve Axthelm <steve@puppet.com>

RUN apt update
RUN apt install curl -y
RUN apt install ca-certificates gnupg -y
RUN curl https://www.postgresql.org/media/keys/ACCC4CF8.asc | gpg --dearmor | \
  tee /etc/apt/trusted.gpg.d/apt.postgresql.org.gpg >/dev/null

RUN echo "deb http://apt.postgresql.org/pub/repos/apt bookworm-pgdg main" > /etc/apt/sources.list.d/pgdg.list

RUN apt update
RUN apt-get install postgresql-17-pglogical

# VOLUME /var/lib/postgresql/data # re-volume this so that the config file changes take???

RUN echo "host    replication          postgres                172.18.0.0/16   trust" >> /usr/share/postgresql/17/pg_hba.conf.sample
RUN echo "host    replication          postgres                ::1/128         trust" >> /usr/share/postgresql/17/pg_hba.conf.sample
RUN echo "shared_preload_libraries = 'pglogical'" >> /usr/share/postgresql/postgresql.conf.sample
RUN echo "wal_level = 'logical'" >> /usr/share/postgresql/postgresql.conf.sample
RUN echo "max_wal_senders = 20" >> /usr/share/postgresql/postgresql.conf.sample
RUN echo "max_replication_slots = 20" >> /usr/share/postgresql/postgresql.conf.sample
RUN echo "max_connections = 600" >> /usr/share/postgresql/postgresql.conf.sample
# uncomment this to see the full logs
# RUN echo "log_statement = 'all'" >> /usr/share/postgresql/postgresql.conf.sample

COPY primary.sql /docker-entrypoint-initdb.d/init.sql
