# cvsserver
git clone https://github.com/infracloudio/csvserver.git
cd csvserver/solution
nano gencsv.sh

chmod +x gencsv.sh
./gencsv.sh 2 8
docker stop infra
docker rm infra
docker run --name infra -d -p 9393:9300 -v "$(pwd)/inputFile:/csvserver/inputdata" infracloudio/csvserver:latest
docker logs infra
curl http://localhost:9393
docker stop infra
docker rm infra
docker run --name infra -d -p 9393:9300 -v "$(pwd)/inputFile:/csvserver/inputdata" -e CSVSERVER_BORDER=Orange infracloudio/csvserver:latest
