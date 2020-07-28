# DESCRIPTION:	  Create a Simple Tmux and NeoVim Development Enviornment
# AUTHOR:		  Jason McDonald <JMcDon31@gmail.com>
# COMMENTS:
#		This Dockerfile builds an image that can be used for basic
#		neovim deveopment
# USAGE:
#	#Build Image	
# 		docker image build 	https://github.com/jmcdon31/Dockerfiles.git#master:devenv \
# 					--build-arg USER_ID=$(id -u ${USER}) \
# 					--build-arg GROUP_ID=$(id -g ${USER}) \
# 					--build-arg USER_NAME=${USERNAME} \
# 					-t devenv 
#
#			# Must supply there USER params to prevent opening a
#			xhost ACL to all local traffic. This gives us full
#			Clipboard Support
#
#	#Run Container at Current Directory
#		docker run --rm -it \
#				-e DISPLAY \
#				-v $PWD:$PWD \
#				-v /tmp/.X11-unix:/tmp/.X11-unix \
#				--user=$(id -u $USER):$(id -g $USER) \
#				devenv
#
#
#	
#	${PWD##*/} - Parameter Expansion to get just the current directory name
#		     without the full path
#

# Base Image
FROM ubuntu:20.04

ARG USER_NAME
ARG USER_ID
ARG GROUP_ID

RUN 	groupadd -g ${GROUP_ID} ${USER_NAME} && \
	useradd -l -u ${USER_ID} -g ${USER_NAME} ${USER_NAME} && \
	install -d -m 0755 -o ${USER_NAME} -g ${USER_NAME} /home/${USER_NAME}

WORKDIR	/home/${USER_NAME}

RUN apt-get update 		&& \
    apt-get install -y neovim   && \
    apt-get install -y tmux 	&& \
    apt-get install -y curl 	&& \
    apt-get install -y git 	&& \
    apt-get install -y sudo 	&& \
    apt-get install -y bash-completion

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Set password for user so sudo can work in container
RUN echo "${USER_NAME}:docker" | chpasswd && adduser ${USER_NAME} sudo

# sudo: setrlimit(RLIMIT_CORE): Operation not permitted workaround
RUN touch  /etc/sudo.conf && \
    echo "Set disable_coredump false" >> /etc/sudo.conf

USER ${USER_NAME}

# Setup neovim with my vimrc and desired colorscheme
RUN mkdir -p .config/nvim/colors && \
    cd .config/nvim/colors && \
    curl -O -J https://raw.githubusercontent.com/altercation/vim-colors-solarized/master/colors/solarized.vim && \
    cd .. && curl -O -J https://raw.githubusercontent.com/jmcdon31/workflowfiles/master/init.vim && \
    cd ../../ && curl -O -J https://raw.githubusercontent.com/jmcdon31/workflowfiles/master/.bashrc && \
    curl -O -J https://raw.githubusercontent.com/jmcdon31/workflowfiles/master/.tmux.conf   && \
    touch .bash_profile && echo "source ~/.bashrc" >> .bash_profile

# Setup Git globals
RUN   	git config --global user.email "jmcdon31@gmail.com"  && \
  	git config --global user.name "Jason McDonald"

ENTRYPOINT [ "bash" ]
