# DESCRIPTION:	  Create a Simple Tmux and NeoVim Development Enviornment
# AUTHOR:		  Jason McDonald <JMcDon31@gmail.com>
# COMMENTS:
#		This Dockerfile builds an image that can be used for basic
#		neovim deveopment
# USAGE:
#	#Build Image	
#	docker build https://github.com/jmcdon31/Dockerfiles.git#master:devenv -t devenv
#
#	#Run Container at Current Directory
# 	docker run -it  -v $PWD:/root/${PWD##*/} devenv
#	
#	${PWD##*/} - Parameter Expansion to get just the current directory name
#		     without the full path
#


# Base Image
FROM ubuntu:20.04

WORKDIR	/root/

RUN apt-get update 		&& \
    apt-get install -y neovim   && \
    apt-get install -y tmux 	&& \
    apt-get install -y curl 

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Setup neovim with my vimrc and desired colorscheme
RUN mkdir -p .config/nvim/colors && \
    cd .config/nvim/colors && \
    curl -O -J https://raw.githubusercontent.com/altercation/vim-colors-solarized/master/colors/solarized.vim && \
    cd .. && curl -O -J https://raw.githubusercontent.com/jmcdon31/workflowfiles/master/init.vim

# When Bash starts make sure its in Vi mode with neovim set as the editor
RUN echo -e 'set -o vi\nexport EDITOR="/usr/bin/nvim"' >> ~/.bashrc

ENTRYPOINT [ "bash" ]
