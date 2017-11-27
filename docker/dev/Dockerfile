FROM lpmulligan/todobackend-base:latest
MAINTAINER Lawrence Mulligan <lmulligan@lpmnet.com>

# Install dev/build dependencies
RUN apt-get update && \
    apt-get install -qy gcc python-dev libmysqlclient-dev

# Activate virtual environment and install whell support
RUN . /appenv/bin/activate && \
    pip install wheel --upgrade

# PIP Environment variables (NOTE: must be set after installing wheel)
ENV WHEELHOUSE=/wheelhouse PIP_WHEEL_DIR=/wheelhouse PIP_FIND_LINKS=/wheelhouse XDG_CACHE_HOME=/cache

# OUTPUT: Build artifacts (Wheels) are output here
VOLUME /wheelhouse

# OUTPUT: Build cache
VOLUME /build

# Output: Test reports are output here
VOLUME /reports

# Add test entrypoint script
COPY scripts/test.sh /usr/local/bin/test.sh
RUN chmod +x /usr/local/bin/test.sh

# Set defautls for entrypoint and comman string
ENTRYPOINT [ "test.sh" ]
CMD ["python", "manage.py", "test", "--noinput"]

# Add application source
COPY src /application
WORKDIR /application