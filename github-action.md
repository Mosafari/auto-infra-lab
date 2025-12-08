Github Action -
1. you need a linux runner.
2. ansible and ansible core installed
(if you provisioned server manually)
  ?. create ssh key with `ssh-keygen` and login to your provisioned servers via root user
3. add K8S-USER to secrets in github action (the root user in my case for my provisioned servers)
