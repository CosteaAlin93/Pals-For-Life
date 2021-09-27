## Task 1 Deploy the VM


Please allow 5 minutes for the machine to fully boot up.

> Answer: No answer needed


## Task 2 Compromise the machine



**Answer the questions below**

### Flag 1

`export ip=10.10.219.14`

`ping $ip`

- Get machine IP and check the connectivity:

![image](https://user-images.githubusercontent.com/86648102/134903424-aebdd489-9e4f-4471-b155-6eeade692bc6.png)
- Scanning and Enumeration:
`sudo nmap -sC -sV -v -oN PalsForLifenmapscan.txt $ip -p- -Pn`

Open ports:
- 22 ssh
- 6443 ssl/sun-sr-https? Kubernetes
- 10250 Golang net/http server
- 30180 nginx
- 31111 Gitea (Git with a cup of tea) is a painless self-hosted Git service written in Go
- 31112 OpenSSH

---
- For now, we leave the SSH ports alone. The most interesting, in my oppinion is the Gitea 31111 port.

![image](https://user-images.githubusercontent.com/86648102/134904400-5e3ce142-048b-43c0-a60f-170e9f45d32a.png)
