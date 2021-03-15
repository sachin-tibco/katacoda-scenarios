
Create a directory "cow-test"

`mkdir cow-test`{{execute}}

`cd cow-test`{{execute}}

`touch Dockerfile.base`{{execute}}
`touch Dockerfile`{{execute}}
`touch hello.sh`{{execute}}

Dockerfile.base
<pre class="file"
 data-filename="/root/cow-test/Dockerfile.base"
  data-target="replace">
  	FROM ubuntu:18.04
	COPY . /app
</pre>

Dockerfile
<pre class="file"
 data-filename="/root/cow-test/Dockerfile"
  data-target="replace">
  	FROM acme/my-base-image:1.0
	CMD /app/hello.sh
</pre>



hello.sh

Dockerfile
<pre class="file"
 data-filename="/root/cow-test/hello.sh"
  data-target="replace">
  	#!/bin/sh
	echo "Hello world"
</pre>
