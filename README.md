####Dokumentation der automatisch aufsetzbaren Systemlandschaft
#
#
# Durch die verschiedenen Docker Compose Files kann varaiable ausgewählt werden, welche Teile der Continouse Integration Systemlandschaft
# Installiert werden sollen. 
#  1.
#  2.

    #!/bin/bash
    # Delete all containers
    docker rm $(docker ps -a -q)
    # Delete all images
    docker rmi $(docker images -q)
	#Delete all Volumes 
	docker volume rm $(docker volume ls)
	#Stoppe alle aktiven Dockercontainer
	docker stop $(docker ps -a)
	
	
	