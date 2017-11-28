FROM lpmulligan/todobackend-base:latest
MAINTAINER Lawrence Mulligan <lmulligan@lpmnet.com>

# Copy application artifacts
COPY target /wheelhouse

# Install application
RUN . /appenv/bin/activate && \
    pip install --no-index -f /wheelhouse todobackend && \
    rm -rf /wheelhouse