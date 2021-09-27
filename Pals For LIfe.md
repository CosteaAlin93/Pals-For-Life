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

- Let's explore the website. Under **Explore** > **Users** we manage to find the following:
![image](https://user-images.githubusercontent.com/86648102/134904776-cd8e3428-448e-430e-8c58-e69f489facbb.png)

We have a user: leeroy.

---

- I tried scanning the other ports with Gobuster, to see if other pages are around there. The 30180 returned something interesting:

`sudo gobuster dir -u http://$ip:30180 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt | tee palsforlifegobuster.txt`

![image](https://user-images.githubusercontent.com/86648102/134906394-ffd3def6-6fee-48b8-a87f-9e332c3d506a.png)

http://machineip:30180/team 

![image](https://user-images.githubusercontent.com/86648102/134906568-0b0dbb54-8df7-4aaf-8e81-770fda5571bf.png)

Someone seems to like World Of Warcraft a lot :)

Nothing special on the page, except the video. However, when inspecting the page:

![image](https://user-images.githubusercontent.com/86648102/134906809-ee1d0239-2d66-439e-bae9-10185e572e1c.png)


Someone forgot an "uninteresting" file around.


