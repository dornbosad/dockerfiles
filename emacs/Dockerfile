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
#	docker run -d \
#	        -v /tmp/.X11-unix:/tmp/.X11-unix \
#               -v /etc/localtime:/etc/localtime:ro \
#               -v $HOME/git/orgfiles:$HOME/git/orgfiles
#               -v $HOME/git/orgbinder:$HOME/git/orgbiner
#		-e DISPLAY=unix$DISPLAY emacs

# Base docker image
FROM debian:bullseye-slim
LABEL maintainer "Aaron Dornbos <dnrbs@airmail.cc>"

# Install Emacs and its dependencies
RUN apt-get update && apt-get install -y \
    emacs \
    git \
    make \
    --no-install-recommends \
    && rm -rf /var/lib/apt/lists/*

# Grab configuration deps from repo
RUN mkdir ~/git \
    ~/git/orgbinder \
    ~/git/orgfiles \
    ~/git/orgfiles/p \
    cd ~/git/ \
    git clone https://code.orgmode.org/bzg/org-mode.git
    cd org-mode/ \
    make autoloads \
    cd ~/ \
    git clone https://github.com/dornbosad/.emacs.git
    git clone https://github.com/dornbosad/.fonts.git

#   Autorun emacs
ENTRYPOINT ["emacs"]

#   Please note that getStarted.el will need to be ran first via M-x load-file RET ~/.emacs/getStarted.el
#   Followed by M-x package-refresh-contents RET, M-x install-package RET use-package
#   Finally M-x load-file RET ~/.emacs/init.el
