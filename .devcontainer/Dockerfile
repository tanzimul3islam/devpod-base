FROM mcr.microsoft.com/devcontainers/base:ubuntu-24.04

# Rename the 'vscode' user to 'david'
ARG USERNAME=tanzimul
RUN usermod -l $USERNAME vscode && \
    usermod -m -d /home/$USERNAME $USERNAME && \
    groupmod -n $USERNAME vscode

# Install the curl, vim and, tmux packages
RUN apt-get update && apt-get install -y curl vim tmux alacritty

COPY --from=jdxcode/mise /usr/local/bin/mise /usr/local/bin/

# make sure mise is activated in both zsh and bash. Might be overridden by a user's dotfiles.
RUN echo 'eval "$(mise activate bash)"' >> /home/$USERNAME/.bashrc && \
    echo 'eval "$(mise activate zsh)"' >> /home/$USERNAME/.zshrc

# Give the non-root use sudo access

RUN apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME
#
# # ********************************************************
# # * Anything else you want to do like clean up goes here *
# # ********************************************************
#
# # [Optional] Set the default user. Omit if you want to keep the default as root.
USER $USERNAME
