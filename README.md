# Change the location of docker images root for Docker Desktop on WSL2 with Windows 10 

1. First, shut down your docker desktop by right click on the Docker Desktop icon and select Quit Docker Desktop \
2. Then, open your command prompt:
```
wsl --list -v
```

You should be able to see, make sure the STATE for both is Stopped.
```
wsl --shutdown
```
```
  NAME               	  STATE       	VERSION
* docker-desktop     	  Stopped     	2
  docker-desktop-data     Stopped     	2
```
\
3. Export docker-desktop-data into a file
```
wsl --export docker-desktop-data "D:\Docker\wsl\data\docker-desktop-data.tar"
```
\
4. Unregister docker-desktop-data from wsl. The ext4.vhdx file would automatically be removed (so back it up first if you have important existing image/container):
```
wsl --unregister docker-desktop-data
```
\
5. Import the docker-desktop-data back to wsl, the ext4.vhdx would reside in the new drive/directory:
```
wsl --import docker-desktop-data "D:\Docker\wsl\data" "D:\Docker\wsl\data\docker-desktop-data.tar" --version 2
```
\
6. Start the Docker Desktop again and it should work. (You may delete the D:\Docker\wsl\data\docker-desktop-data.tar file)

