
Create a directory "cow-test"

`mkdir cow-test`{{execute}}

`cd cow-test`{{execute}}

`vi Dockerfile.base`{{execute}}

Dockerfile.base
<pre class="file"
 data-filename="/root/cow-test/Dockerfile.base"
  data-target="copy">
  	FROM ubuntu:18.04
	COPY . /app
</pre>

Dockerfile
<pre class="file"
 data-filename="/root/cow-test/Dockerfile"
  data-target="copy">
  	FROM acme/my-base-image:1.0
	CMD /app/hello.sh
</pre>



hello.sh

Dockerfile
<pre class="file"
 data-filename="/root/cow-test/hello.sh"
  data-target="copy">
  	#!/bin/sh
	echo "Hello world"
</pre>
