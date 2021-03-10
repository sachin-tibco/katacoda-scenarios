we need to create a docker image for the voting app so we will go into vote directory

`cd vote`{{execute}}

python based Dockfile for the voting app
`cat Dockerfile`{{execute}}

Buld the voting app and tagged as "voting-app"

`docker build . -t voting-app`{{execute}}

New image of voting-app created you  can see by images list command

`docker images`{{execute}} 

Run the voting-app and publish a port to 5000 to 80 

`docker run -p 5000:80 voting-app`{{execute}}



