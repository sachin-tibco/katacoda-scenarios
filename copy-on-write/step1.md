
Create a directory "cow-test"

`mkdir cow-test`{{execute}}

`cd cow-test`{{execute}}

`vi Dockerfile.base`{{execute}}

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



