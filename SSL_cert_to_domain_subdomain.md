
### SSL certificate to subdomian 

**Note**: subdomains can use SSL of main domain. 

Check with support and Activate SSL from home page    
![Capture](https://user-images.githubusercontent.com/29883334/97824049-e1b63980-1ce0-11eb-96d8-1b9cdb2ee5c0.PNG)


### SSL certificate to subdomian mapped to VPS ip ( ex: api.whathefun.in ):

@ Create a virtual server/host in virtualmin tab from webmin dashboard.      
**Note:** By the end Make sure SSL certificate feature is enabled  

@ update UI theme if Create Virtual Server is not visible.   

![after-update-webmin-theme-create-server-visible](https://user-images.githubusercontent.com/29883334/97823691-baab3800-1cdf-11eb-8180-445e7acffbf7.png)


@ create virtual server.  
1. give subdomain name in hostname field (SSL can't be given to private ip address)  (ex: **app.whathefun.in)  
2. make sure SSL selected  
![creating-virtual-server](https://user-images.githubusercontent.com/29883334/97702172-8e6f9b80-1ad4-11eb-9ea6-e8d9b074e76f.png)

@ check virtual server ip. change it if not matched to the host.  
![vir-serv-changed-ip-to](https://user-images.githubusercontent.com/29883334/97823241-5cca2080-1cde-11eb-9019-e436ef55be10.PNG)

@ It's time to Request Certificate:  
```Virtualmin -> Server Configuration -> SSL Certificate -> Let's Encrypt```  

![api-ssl-cert](https://user-images.githubusercontent.com/29883334/97823534-4a9cb200-1cdf-11eb-9e61-a187cd96f7b0.PNG)

@ Request Certificate success messages  
![ssl-cert-success-for-api-whathefun](https://user-images.githubusercontent.com/29883334/97823808-0b229580-1ce0-11eb-969c-20af36674da0.PNG)

@ SSL Cert added to subdomain which is mapped to VPS. (backend is up and running on the ip)  
![fully-encrypted-api](https://user-images.githubusercontent.com/29883334/97824262-7456d880-1ce1-11eb-8f02-f1ac47987b61.PNG)

