####Dokumentation des automatisch aufsetzbaren Jenkins CI Servers
#
#
Durch die verschiendenen dockerfiles in den einzelnen Ordnern kann ausgewählt werden welcher Jenkins mit welcher Beispielapplikation installiert und Konfiguriert werden soll. 

Es gibt die Folgenden varianten:
1. Jenkins CI Server mit Java und maven
2. Jenksins CI Server mit Android und Gradle
3. Jenkins CI Server mit iOS und Fastlane

bei den Beispielapplikationen handelt es sich jeweils um ein Hello world, da es dabei nur darum geht die Umgebung für eine jeweilige ConfigurationsUmgebung herrichten zu können. 


Weitere allgemein brauchbare Docker Comandos zum steuern des Jnekins containers:
    #!/bin/bash
    # Delete all containers
    docker rm $(docker ps -a -q)
    # Delete all images
    docker rmi $(docker images -q)
	#Delete all Volumes 
	docker volume rm $(docker volume ls)
	#Stoppe alle aktiven Dockercontainer
	docker stop $(docker ps -a)
	
	
	