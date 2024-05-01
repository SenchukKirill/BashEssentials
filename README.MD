
# Docker


### full clean images command:

example: `docker system prune -a --volumes` 

### Opening ports from server and container

example: `docker run -d -p 80:80 nginx`

if we need opening more then one port in server we can add another port with first argument

example: `docker run -d -p 8080:80 nginx`