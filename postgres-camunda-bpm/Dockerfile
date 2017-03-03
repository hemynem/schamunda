FROM postgres:9.4-alpine
# Camunda is currently supported on PostgreSQL 9.4.
# See also: https://docs.camunda.org/manual/latest/introduction/supported-environments/

# install a wget version that supports SSL and login
RUN apk --no-cache add ca-certificates wget && update-ca-certificates

# no suffix '-ee' in CAMUNDA_VERSION!
ENV CAMUNDA_VERSION 7.6.0

# https://camunda.org/release/camunda-bpm/tomcat/7.6/camunda-bpm-tomcat-7.6.0.tar.gz
#
# download SQL scripts for Camunda BPM
# (All releases contain the same SQL scripts. Oracle WLS is just used to keep the download small.)
RUN wget -O - "https://camunda.org/release/camunda-bpm/tomcat/$(echo $CAMUNDA_VERSION | cut -c 1-3)/camunda-bpm-tomcat-${CAMUNDA_VERSION}.tar.gz" | \
    tar xzf - --directory /docker-entrypoint-initdb.d/ "sql/create/postgres_engine_${CAMUNDA_VERSION}.sql" "sql/create/postgres_identity_${CAMUNDA_VERSION}.sql" --strip 2

