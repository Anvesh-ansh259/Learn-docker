STEPS for overlay network connect 



1=> We need two machine on same vpc and docker installed in it.



2==> **RUN**

docker swarm init --advertise-addr <PRIVATE-IP>   => It will initialize the swarm 



and it gives the output worker join 



docker swarm join --token <token> <PRIVATE-IP>:2377   ==> Like this 



3==> Security group need to be updated on the both machine for 



2377   -- Swarm Cluster Management (manager <-> worker)  => TCP

7946 -- Node communication => TCP nd UDP

4789 --- Overlay network ==> TCP



4==> **In the machine 2 RUN** 



sudo docker swarm join --token <token> <Machine1-PRIVATE-IP>:2377   ==> This command we will get it on machine 1



output should show **This node joined a swarm as a worker.**



5==> on machine 1 RUN 



docker node ls



it should show both node in different hostname



6==> **Create Overlay Network**



docker network create -d overlay mynet





7==> **Deploy two test services**



docker service create --name web1 --network mynet alpine sleep infinity



docker service create --name web2 --network mynet alpine sleep infinity



8==>  **Check the connectivity** 



docker ps



docker exec -it <containerID> sh



ping web2







