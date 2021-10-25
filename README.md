# openshift-install-config

````
apiVersion: v1
baseDomain: clusterfudge.net
compute:
- architecture: amd64
  hyperthreading: Enabled
  name: worker
  platform:
    vsphere:
      cpus: 4 ## CPU for work nodes
      coresPerSocket: 2
      memoryMB: 20480 ## RAM for worker nodes
      osDisk:
        diskSizeGB: 200
  replicas: 3
controlPlane:
  architecture: amd64
  hyperthreading: Enabled
  name: master
  platform:
    vsphere:
      cpus: 4 ## CPU for controlplane nodes
      coresPerSocket: 2
      memoryMB: 20480 ##RAM for controlplane nodes
      osDisk:
        diskSizeGB: 200 
  replicas: 3
metadata:
  name: ## cluster name 
networking:
  clusterNetwork:
  - cidr: 10.128.0.0/14 ## Network that pods use
    hostPrefix: 23
  machineNetwork:
  - cidr: ## Enter network CIDR address 
  networkType: OpenShiftSDN
  serviceNetwork:
  - 172.30.0.0/16 ## Service network
platform:
  vsphere:
    apiVIP: ## IP address api.<cluster_name>.<base_domain>
    ingressVIP: ## IP address of *.apps.<cluster_name>.<base_domain> 
    cluster: ## cluster name
    datacenter: ## datacenter name
    defaultDatastore: ## datastore name
    network:  ## portgroup where cluster will be deployed
    username: 'ocpadmin@vsphere.local' ##Account/Service Account to use for provisioning
    password: 'ocpOMGOCPomg' ##Password for Account/Service Account
    vCenter: ## FQDN of vCenter server
    clusterOSImage: http://bastion.redhat.io/rhcos-vmware.x86_64.ova
publish: Internal
fips: true
pullSecret: '{"auths":{"bastion.redhat.local:5000":{"auth":"123456789="}}}' ## Replace with your registry and credential  
imageContentSources:
- mirrors:
  - bastion.redhat.local:5000/openshift/release
  source: quay.io/openshift-release-dev/ocp-release
- mirrors:
  - bastion.redhat.local:5000/openshift/release
  source: quay.io/openshift-release-dev/ocp-v4.0-art-dev
sshKey: 'ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAA.....
additionalTrustBundle: |
  -----BEGIN CERTIFICATE-----
  MIIFnzCCA4egAwIBAgIUb5wmeybqQeJv6Zi04zNPGMI737IwDQYJKoZIhvcNAQEL
  BQAwXzEaMBgGA1UEAwwRdXRpbGl0eS5yZWRoYXQuaW8xEDAOBgNVBAoMB1JlZCBI
  YXQxFTATBgNVBAcMDERlZmF1bHQgQ2l0eTELMAkGA1UECAwCVFgxCzAJBgNVBAYT
  < .... omitted .... >
    -----END CERTIFICATE-----
````
