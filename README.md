1. Create Azure VM with UbuntuLTS
 
   E.g: 

   az vm create -n azvdockn01 -g azrgn01 --image UbuntuLTS --no-wait

2. Install docker.io

   apt install docker.io -y

3. Verify if docker is running correctly

   docker info
   docker ps

4. Open port 80 on this VM

   az vm open-port -g azrgn01 -n azrgn01 --port 80

5. Clone GIT repo

   cd ~
   git clone https://github.com/pamvdam/docker-hw2.git
   cd docker-hw

6. Build the container image.

   docker build . --tag helloworld:rc1

   We tag the image to make it recognizable. The part after the ':' can be used for a release tag part.
   In this case RC1 -> Release Candidate 1.

   Ech line in the Dockerfile will result in a layer in the image.

7. Check if the image is available now.

   docker images

8. Try to run the image in a container

   docker run -d -p 80:8081 --name myhelloworld helloworld:rc1

9. Check with links or elinks if the app is available.

   links http://localhost

   As port 80 has been openend in the Azure FW you can also point your browser to the external IP adres.

   Check with:

   az vm list -d -o table
   firefox http://<external-ipaddr>

10. Change the logo in the helloworld.js file.

    Edit helloworld.js and change the logo as specified in the line:

    res.send('<img src="/logo.svg" width=200px><H1>Hello World!</H1><br>Serving you from '+hostname+' <br>You are visitor: #'+visitorCount+' and coming from '+visitorAddr+'<br>Container is up for '+(t_now-t_start)+' ms') ;

    You can relace /logo.svg with any logo available in the public directory

    e.g:

    res.send('<img src="/Azure.png" width=200px><H1>Hello World!</H1><br>Serving you from '+hostname+' <br>You are visitor: #'+visitorCount+' and coming from '+visitorAddr+'<br>Container is up for '+(t_now-t_start)+' ms') ;

11. Rebuild the docker image

    docker build . --tag helloworld:rc2

12. Check if the new image is available now.

    docker images

13. Try to run the newer version in a container

   docker run -d -p 80:8081 --name myhelloworld helloworld:rc2

14. Check the result with links and/or the browser on your laptop.
