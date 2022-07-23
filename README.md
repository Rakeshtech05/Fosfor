#!/bin/bash


rm -rf /home/centos/FOSFOR/appserver/solution/inputFile
for i in {0..10}
  do
     echo "$i","" "$RANDOM" >> inputFile
done
docker run -d -p 8080:9300 docker.io/fosfordevops/csvgenerator sleep infinity
id=$(docker ps -a | awk 'FNR == 2 {print $1}')
docker cp /home/centos/FOSFOR/appserver/solution/inputFile "$id":/csvserver/inputFile
