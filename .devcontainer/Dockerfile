# Copyright (c) 2024 RFull Development
# This source code is managed under the MIT license. See LICENSE in the project root.
FROM ryotafunaki/devcontainer-dotnet:sdk-8.0-aspire

# Install development tools for root
USER root
WORKDIR /root

# Install development tools for root
COPY ./shells/root/ ./shells/
RUN cd ./shells && \
    chmod +x install.sh && \
    ./install.sh && \
    cd ..
RUN rm -rf ./shells

# Switch to the non-root user
ARG USER_NAME=developer
USER ${USER_NAME}
WORKDIR /home/${USER_NAME}

# Install development tools for non-root
COPY --chown=${USER_NAME}:${USER_NAME} ./shells/user/ ./shells/
RUN cd ./shells && \
    chmod +x install.sh && \
    ./install.sh && \
    cd ..
RUN rm -rf ./shells

USER root

# Clean up
RUN apt clean && \
    rm -rf /var/lib/apt/lists/*
RUN rm -rf /tmp/* && \
    rm -rf /var/tmp/*

USER ${USER_NAME}
WORKDIR /home/${USER_NAME}
