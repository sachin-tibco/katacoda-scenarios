
Create a directory "cow-test"

`mkdir cow-test`{{execute}}

`cd cow-test`{{execute}}

Creating two Dockerfiles - Dockerfile.base and Dockerfile
Using the first one to create an image called acme/my-base-image:1.0

`touch Dockerfile.base`{{execute}}


The second one is based on acme/my-base-image:1.0, but has some additional layers:

`touch Dockerfile`{{execute}}


`touch hello.sh`{{execute}}


Open and copy below content to Dockerfile.base

`/root/cow-test/Dockerfile.base`{{open}}

<pre class="file"
 data-filename="/root/cow-test/Dockerfile.base"
  data-target="replace">
FROM ubuntu:18.04
COPY . /app
</pre>

Open and copy below content to Dockerfile

`/root/cow-test/Dockerfile`{{open}}

<pre class="file"
 data-filename="/root/cow-test/Dockerfile"
  data-target="replace">
FROM acme/my-base-image:1.0
CMD /app/hello.sh
</pre>


Open and copy below content to hello.sh 

`/root/cow-test/hello.sh`{{open}}

<pre class="file"
 data-filename="/root/cow-test/hello.sh"
  data-target="replace">
#!/bin/sh
echo "Hello world"
</pre>

Save the file, and make it executable:

`chmod +x hello.sh`{{execute}}


Build the image from first Dockerfile.base

`docker build -t acme/my-base-image:1.0 -f Dockerfile.base .`{{execute}}


Build the second image from Dockerfile.

`docker build -t acme/my-final-image:1.0 -f Dockerfile .`{{execute}}


Check out the sizes of the images:

`docker image ls`{{execute}}


Check out the layers that comprise each image:

`docker history acme/my-base-image:1.0`{{execute}}


`docker history acme/my-final-image:1.0`{{execute}}


Notice that all the layers are identical except the top layer of the second image. 
All the other layers are shared between the two images, and are only stored once in /var/lib/docker/. 
The new layer actually doesn’t take any room at all, because it is not changing any files, but only running a command.


Image and container layers on-disk

THE IMAGE LAYER 

`ls -l /var/lib/docker/overlay/`{{execute}}

Warning: Do not directly manipulate any files or directories within /var/lib/docker/. These files and directories are managed by Docker.


THE CONTAINER LAYER


`docker run -itd ubuntu sleep 3600`{{execute}}

Containers also exist on-disk in the Docker host’s filesystem under /var/lib/docker/overlay/. If you list a running container’s subdirectory using the ls -l command, three directories and one file exist:

<pre class="file">

$ ls -l /var/lib/docker/overlay/<directory-of-running-container>

total 16
-rw-r--r-- 1 root root   64 Jun 20 16:39 lower-id
drwxr-xr-x 1 root root 4096 Jun 20 16:39 merged
drwxr-xr-x 4 root root 4096 Jun 20 16:39 upper
drwx------ 3 root root 4096 Jun 20 16:39 work
</pre>

The lower-id file contains the ID of the top layer of the image the container is based on, which is the OverlayFS lowerdir.

The upper directory contains the contents of the container’s read-write layer, which corresponds to the OverlayFS upperdir.

The merged directory is the union mount of the lowerdir and upperdir, which comprises the view of the filesystem from within the running container.

The work directory is internal to OverlayFS.

To view the mounts which exist when you use the overlay storage driver with Docker, use the mount command. The output below is truncated for readability.

`mount | grep overlay`{{execute}}



