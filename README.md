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

6. 
