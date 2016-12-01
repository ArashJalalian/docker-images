# Bamboo Dockerfile
# Usage 
docker build -t bamboo .

docker run -it --name bamboo -p 8085:8085 -p 54663:54663 bamboo
