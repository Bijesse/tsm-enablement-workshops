FROM debian:bookworm-slim

ARG USERNAME=demouser
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get update \
    && apt-get install -y sudo jq wget unzip htop curl procps findutils uuid-runtime vim \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

COPY configure_environment.sh /

RUN chmod +x /configure_environment.sh

USER $USERNAME

COPY install_demo.sh /

RUN sudo chmod +x /install_demo.sh

SHELL [ "/bin/bash", "-c" ]

ENV SHELL=/bin/bash