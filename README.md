# Docker Swarm Basic Commands

docker-machine create -d virtualbox manager1

docker-machine create -d virtualbox worker1

docker-machine ssh manager1 "docker swarm init --listen-addr $(docker-machine ip manager1) --advertise-addr $(docker-machine ip manager1)" export manager_token=`docker-machine ssh manager1 "docker swarm join-token manager -q"`export worker_token=`docker-machine ssh manager1 "docker swarm join-token worker -q"`for node in $(seq 1 $workers); do echo "======> worker$node joining swarm as worker ..."; docker-machine ssh worker$node "docker swarm join --token $worker_token --listen-addr $(docker-machine ip worker$node) --advertise-addr $(docker-machine ip worker$node) $(docker-machine ip manager1):2377"; done

docker-machine ssh manager1 "docker node ls"

docker-machine ssh manager1 "docker service create -p 80:80 --name web nginx:latest"

docker-machine ssh manager1 "docker service ls"

Useful link:
https://github.com/docker/labs/tree/master/swarm-mode/beginner-tutorial
