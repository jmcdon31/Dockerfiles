# DESCRIPTION:	 Create a Python Image dev env for image manipulation 
# AUTHOR:		  Jason McDonald <JMcDon31@gmail.com>
# COMMENTS:
#		This Dockerfile builds an image that can be used for basic
#		neovim deveopment
# USAGE:
#	#Build Image	
#		docker image build	https://github.com/jmcdon31/Dockerfiles.git#master:devenv \
#					--build-arg USER_ID=$(id -u ${USER}) \
#					--build-arg GROUP_ID=$(id -g ${USER}) \
#					--build-arg USER_NAME=${USERNAME} \
#					-t py_image_devenv 
#
#			# Must supply there USER params to prevent opening a
#			xhost ACL to all local traffic. This gives us full
#			Clipboard Support
#
#       #Run Container at Current Directory
#sudo docker run --rm -it \
#		-e DISPLAY \
#		-v $PWD:$PWD \
#		-v /tmp/.X11-unix:/tmp/.X11-unix \
#		--user=$(id -u $USER):$(id -g $USER) \
#		py_image_devenv 
#
#
#	
#	${PWD##*/} - Parameter Expansion to get just the current directory name
#		     without the full path
#

# Base Image
FROM devenv

#WORKDIR	/home/${USER_NAME}

USER root

RUN 	apt-get update	&& \
    	apt-get install -y python3-pip  


RUN 	python3 -m pip install --upgrade pip	&& \
	python3 -m pip install --upgrade Pillow	&& \
	python3 -m pip install --upgrade numpy
#ENTRYPOINT [ "bash" ]
