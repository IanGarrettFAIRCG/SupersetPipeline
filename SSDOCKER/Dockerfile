FROM apache/superset:latest

# Switch to root to install dependencies
USER root

# Install additional dependencies if needed
RUN pip install --no-cache-dir \
    psycopg2-binary \
    redis \
    celery

# Copy any custom configuration files
COPY superset_config.py /app/pythonpath/

# Switch back to superset user
USER superset

# Initialize the database
RUN superset db upgrade

# Create admin user
RUN superset fab create-admin \
    --username admin \
    --firstname Superset \
    --lastname Admin \
    --email admin@superset.com \
    --password admin

# Setup roles and permissions
RUN superset init

# Expose port
EXPOSE 8088

# Start Superset
CMD ["superset", "run", "-h", "0.0.0.0", "-p", "8088", "--with-threads", "--reload"]
