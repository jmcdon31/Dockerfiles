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

RUN set -o vi && \
	export EDITOR="/usr/bin/nvim"


ENTRYPOINT [ "bash" ]
