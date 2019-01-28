FROM postgres:11

USER postgres

# Adjust PostgreSQL configuration so that remote connections to the
# database are possible.
#RUN mkdir -p /etc/postgresql/11/main/ && echo "host all  all    0.0.0.0/0  md5" >> /etc/postgresql/11/main/pg_hba.conf
RUN echo "host all  all    0.0.0.0/0  md5" >> /var/lib/postgresql/data/pg_hba.conf
 
# And add ``listen_addresses`` to ``/etc/postgresql/11/main/postgresql.conf``
RUN echo "listen_addresses='*'" >> /var/lib/postgresql/data/postgresql.conf
 
# Expose the PostgreSQL port
EXPOSE 5432
 
# Add VOLUMEs to allow backup of config, logs and databases
VOLUME  ["/etc/postgresql", "/var/log/postgresql", "/var/lib/postgresql"]

RUN    /etc/init.d/postgresql start 
#    psql --command "CREATE USER pgdock WITH SUPERUSER PASSWORD 'pgdock';" && \
#    createdb -O pgdock pgdock
 
# Set the default command to run when starting the container
CMD ["/usr/lib/postgresql/11/bin/postgres", "-D", "/var/lib/postgresql/data", "-c", "config_file=/var/lib/postgresql/data/postgresql.conf"]
