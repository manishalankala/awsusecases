

### Create VPC 

CIDR - 10.0.0.0/26


Then Create VPN (Secure private link IPSec)







### Create Customer Gateway (is represents the on premise end tunnel)


![image](https://user-images.githubusercontent.com/33985509/98975022-e0bdad00-2515-11eb-9568-c28980815121.png)

if its static give the public router IP of on prem server


![image](https://user-images.githubusercontent.com/33985509/98975274-3003dd80-2516-11eb-86e5-ebfc11b2b7e6.png)

if its dynamic






### Virtual private gateway  (is represents the on aws end tunnel)


![image](https://user-images.githubusercontent.com/33985509/98976721-fd5ae480-2517-11eb-80d3-df084ae9a91a.png)

and click attach to VPC






### Create VPN connection

![image](https://user-images.githubusercontent.com/33985509/98977003-59be0400-2518-11eb-9cfb-935799445b03.png)

Static IP prefixes are CIDR range of on prem
