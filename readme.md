FROM node
# set the working directory
# all the command will be executed inside this directly
WORKDIR /app
# COPY package.json /app
# COPY server.js /app
COPY . /app
# compile time command (build the image)
RUN npm install
# it will install all the dependencies from package.json

EXPOSE 3000
# CMD ["nodemon", "server.js"]
CMD ["npm", "start"]


#terminal code -> docker build .

# docker stop container name
# docker remove container name 

# or

# docker remove container name -f 


# to directly commit the changes in the docker we have to use volumes
# - there is a specific type of volume known as Bind Mount 
# - It allows us to sync our file system with /app directory

# So now we have to use new command 
# - docker run -v %cd%:/app -p 3000:3000 -d --name express-container image-name
# for mac/ linux
# - docker run -v ${pwd}:/app -p 3000:3000 -d --name express-container image-name

# docker exec -it container_name bash
# to get inside docker environment


# Bind mount volume and Sync code
- changes won't be reflected /sync in docker
- use volume to solve this
- There is specific type of volume known as Bind Mount
- It allows us to sync our file system with app directory of Docker 

# Now we want some of the file to not sync
    - if we delete any files or folser from our local project then it will sync with /app and delete from Docker as well

# Annoymous volume - Mount anouymous volume
-> docker run -v ${pwd}:/app -v /app/node_module -d -p 3000:3000 --name node-app-container express-app-image

# Run dev environment
- docker-compose -f docker-compose.yaml -f docker-compose-dev.yaml up -d

# Stop dev environment
- docker-compose -f docker-compose.yaml -f docker-compose-dev.yaml down -d

# Run Production environment
- docker-compose -f docker-compose.yaml -f docker-compose-prod.yaml up -d

# Stop Production environment
- docker-compose -f docker-compose.yaml -f docker-compose-prod.yaml down -d

# docker bash
    