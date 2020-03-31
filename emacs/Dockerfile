# DESCRIPTION: Create emacs container with its dependencies

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

# Install Emacs and its dependencies
RUN apt-get update && apt-get install -y \
    emacs \
    && rm -rf /var/lib/apt/lists/*

#   Autorun emacs
CMD ["emacs"]

#   Please note that getStarted.el will need to be ran first via M-x load-file RET ~/.emacs/getStarted.el
#   Followed by M-x package-refresh-contents RET, M-x install-package RET use-package
#   Finally M-x load-file RET ~/.emacs/init.el
