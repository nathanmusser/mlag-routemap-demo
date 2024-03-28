Deploy an ACT Lab using the YAML file found in the [latest release](https://github.com/nathanmusser/mlag-routemap-demo/releases/latest). 

SSH to the automation device in your deployed lab using the credentials arista / arista123! 

Run the following: 

```
sudo dnf install -y python3.11 git
curl -sSL https://github.com/nathanmusser/avd-bootstrap/releases/download/v1.0.2/avd-bootstrap.sh | sh -s -- -p /usr/bin/python3.11 --install
cd ./avd; source venv_avd/bin/activate
git clone https://github.com/nathanmusser/mlag-routemap-demo.git
cd mlag-routemap-demo/
ansible-playbook build.yml deploy.yml reload.yml

```

Wait for the devices to reload. 

To explore the demo connect to agg1 and agg2 and using the following to enable and disable the routemap.

Remove
```
configure
router bgp 65101
   no neighbor MLAG-IPv4-UNDERLAY-PEER route-map RM-MLAG-PEER-IN in

```

Add
```
configure
router bgp 65101
   neighbor MLAG-IPv4-UNDERLAY-PEER route-map RM-MLAG-PEER-IN in

```
