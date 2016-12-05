# Bamboo Dockerfile
Build docker image for Bamboo Server. Bamboo server version can be modified using BAMBOO_VERSION variable. The default version is 5.14.1.
# Usage 
docker build -t bamboo .

docker run -it --name bamboo -p 8085:8085 -p 54663:54663 bamboo
