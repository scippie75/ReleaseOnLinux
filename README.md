# ReleaseOnLinux
Steps on how to release an application on Linux without an IDE to help you with it

## Warning!
This guide is Work In Progress. Do not use! And even if it's finished... Do not use! Use only at your own risk.

## WIP
This guide is Work In Progress. Although it worked on my computer, someone else is having problems with a missing version of GLIBC. I am still trying to find out how to solve this.

## Getting started
First thing I did was install Ubuntu Linux on a VM in VirtualBox (with 3D support) because most games released on Steam/GOG/... will work on it and we will at least have this too. I also installed the VirtualBox Guest Additions.

I created a share between the host and the guest. It gave permission problems, but the solution was here: https://stackoverflow.com/questions/26740113/virtualbox-shared-folder-permissions. In short, add the guest user to vboxsf: sudo adduser $USER vboxsf

We will be releasing libraries with our executable, so we will need to tell Linux about their location. To keep it simple, we will use the path the executable is in: export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:.

My test application uses SDL2 (sdl2-image, sdl2-ttf) and GLEW, so copy the following files in the director: 
- /usr/lib64/libSDL2-2.0.so.0
- /usr/lib64/libSDL2_image-2.0.so.0
- /usr/lib64/libSDL2_ttf-2.0.so.0
- /usr/lib64/libGLEW.so.2.2
- /usr/lib64/libwebp.so.7 (I don't know why I need this, I don't have any .webp images in my project, maybe SDL needs it)

Try out the executable from the command line and it should work (it didn't work for me as my game requires GLSL 1.50 and VirtualBox doesn't support it).

Create a file start.sh with the following line: echo "LD_LIBRARY_PATH=$LD_LIBRARY_PATH:. ./test" >start.sh
Make it executable: chmod +x start.sh

From now on the application should be able to start by starting start.sh

Optionally, you can move the libraries into a Lib directory or something like that.
