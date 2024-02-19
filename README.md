# k0s

Links:
- https://k0sproject.io/
- https://docs.k0sproject.io/stable/
- https://docs.k0sproject.io/stable/install/
- https://github.com/k0sproject/k0s/releases
- https://github.com/k0sproject/k0sctl/releases

Usage:
```bash
# windows 11 
choco install virtualbox
choco install vagrant
# restart


# versions
VBoxManage.exe -V
7.0.14r161095
vagrant version
Installed Version: 2.4.1


# clone
cd ~/workspace/prwnd9
git clone git@github.com:prwnd9/k0s.git
cd k0s


# SINGLE NODE SETUP

# provision
vagrant up
vagrant ssh
sudo k0s status
sudo k0s kubectl get nodes


# test
sudo k0s kubectl apply -f whoami.yaml
sudo k0s kubectl get deploy
sudo k0s kubectl get svc
sudo k0s kubectl get deploy whoami -o yaml | less
curl 192.168.56.10:30000


# stop or teardown
vagrant halt
vagrant destroy


# CLUSTER SETUP

cd cluster
vagrant up
vagrant ssh
```

