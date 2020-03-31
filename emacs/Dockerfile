# DESCRIPTION:	  Create emacs container with its dependencies
# AUTHOR:		  Aaron Dornbos <drnbs@airmail.cc>
# COMMENTS:
#	This file describes how to build an emacs container with all
#	dependencies installed. It uses native X11 unix socket.
#	Includes font, folder struct, and other dependencies for .config.
#	Tested on Debian Jessie
# USAGE:
#	# Download emacs Dockerfile
#	wget https://raw.githubusercontent.com/dornbosad/dockerfiles/master/emacs/dockerfile
#
#	# Build emacs image
#	docker build -t emacs .
#
#	docker run -v /tmp/.X11-unix:/tmp/.X11-unix:ro \
#	       -e DISPLAY="unix$DISPLAY" \
#	       -e UNAME="emacser" \
#	       -e GNAME="emacsers" \
#	       -e UID="1000" \
#	       -e GID="1000" \
#	       -v <path_to_.emacs>:/home/.emacs \
#	       -v <path_to_workspace>:/mnt/workspace
#               

# Base docker image
FROM debian:bullseye-slim
LABEL maintainer "Aaron Dornbos <dnrbs@airmail.cc>"
ENV NO_AT_BRIDGE=1

# Install Emacs and its dependencies
RUN apt-get update && apt-get install -y \
    emacs \
    --no-install-recommends \
    && rm -rf /var/lib/apt/lists/*

#   Autorun emacs
ENTRYPOINT ["/usr/local/sbin/"]
CMD ["bash", "-c", "emacs; /bin/bash"]

#   Please note that getStarted.el will need to be ran first via M-x load-file RET ~/.emacs/getStarted.el
#   Followed by M-x package-refresh-contents RET, M-x install-package RET use-package
#   Finally M-x load-file RET ~/.emacs/init.el
