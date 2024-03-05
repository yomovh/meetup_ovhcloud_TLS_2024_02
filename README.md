# Notes for the demo that illustrates the talk "How to industrialise the deployment of your solutions with OVHcloud ?"

## OVHcloud control panel interface

Copy public key
```bash
cat ~/.ssh/id_rsa.pub |pbcopy	
```
Add [cloud-init script](./cloud-init.yaml)


## API portal 

[api.ovh.com](https://api.ovh.com)


## Python API 

[Documentation first steps with API](https://help.ovhcloud.com/csm/en-gb-api-getting-started-ovhcloud-api?id=kb_article_view&sysparm_article=KB0042784) provides link to [token creation page](https://eu.api.ovh.com/createToken/)

The following environment variables needs to be filled: 

```
OVH_ENDPOINT=ovh-eu
OVH_APPLICATION_KEY=
OVH_APPLICATION_SECRET=
OVH_CONSUMER_KEY=
```

Install the python OVHCloud wrapper ([github page](https://github.com/ovh/python-ovh))
```bash
python3 -m venv /home/ubuntu/venv
source venv/bin/activate
pip install ovh 
```
 
## Openstack CLI 

From Manager, open the *Horizon* link, Identity > Application Credentials > Create Application Credentials 
scp the file content on the environment, source it. 

```bash
pip install python-openstackclient
openstack server list
```


## Terraform / opentofu

Example from this [project](https://github.com/yomovh/tf-at-ovhcloud)

```bash 
git clone https://github.com/yomovh/tf-at-ovhcloud
```

Add the variable to a file `variables.tfvars`
```
dns_zone                          = "galsandbox.ovh"
acme_email_address                = ""
instance_nb = 4
ovh_public_cloud_project_id = “”
```


Init the providers
```bash
tofu init
```
Launch code
```bash
tofu apply -var-file=variables.tfvars
```

Get avnadmin password from MacOS
```bash
ssh ubuntu@IP 'cd tf-at-ovhcloud/simple_http_lb_with_prom_grafana && tofu output -raw grafana_password'|pbcopy
```