# DESCRIPTION:	  Create a Simple Tmux and NeoVim Development Enviornment
# AUTHOR:		  Jason McDonald <JMcDon31@gmail.com>
# COMMENTS:
#		This Dockerfile builds an image that can be used for basic
#		neovim deveopment
# USAGE:
#	
#	docker build https://github.com/jmcdon31/Dockerfiles.git#master:BasicDevEnv -t basicdevenv
#
#	docker run -v /tmp/.X11-unix:/tmp/.X11-unix \
#		-e DISPLAY=unix$DISPLAY atom
#



FROM ubuntu:20.04

WORKDIR	/root/

RUN apt-get update 		&& \
    apt-get install -y neovim   && \
    apt-get install -y tmux 	&& \
    apt-get install -y curl 


RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


RUN mkdir -p .config/nvim/colors && \
    cd .config/nvim/colors && \
    curl -O -J https://raw.githubusercontent.com/altercation/vim-colors-solarized/master/colors/solarized.vim && \
    cd .. && curl -O -J https://raw.githubusercontent.com/jmcdon31/workflowfiles/master/init.vim

RUN echo $'set -o vi\nexport EDITOR="/usr/bin/nvim"'


ENTRYPOINT [ "bash" ]
