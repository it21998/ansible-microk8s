# Prerequisites
* Installs on local machine that runs the playbooks
* Microk8s install
```bash
sudo snap install microk8s --classic
sudo ufw allow in on eth0 && sudo ufw allow out on eth0
sudo ufw default allow routed
```
* enable in microk8s
```bash
microk8s enable dns ingress storage
microk8s enable dashboard
```
* access without sudo
```bash
sudo usermod -a -G microk8s $USER
sudo chown -f -R $USER ~/.kube

su - $USER
```
# Possible tweaking code
* hosts.yml
```yaml
deploymentmicrok8s:
  hosts:
    microk8s:
      ansible_host: 20.216.31.6
      ansible_port: 22
      ansible_ssh_user: azureuser
      #ansible_ssh_private_key_file= ~/.ssh/id_rsa.pub
```
# Open ports on azure
* 8000
* 9000
* 80
* 8025
* 16443
* 30191

# Ready to run playbooks
```bash
ansible-playbook playbooks/django-install-microk8s.yml
ansible-playbook playbooks/django2-install-microk8s.yml
```
# Url connections
```yaml
django-21998.cloudns.ph #admin
django2-system.ddns.net #system
20.216.31.6:30191 #mailhog
```
