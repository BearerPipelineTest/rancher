# Provisioning Configs
These are the examples of the configurations needed to run the provisioning packages tests. Which includes; RKE2 node driver and custom cluster provisioning, and hosted provider provisioning tests. The examples below are written in JSON, but thee framework also supports YAML.

## RKE1 Provisioning Configs

---

### Provisioning Input
provisioningInput is needed to the run the RKE1 tests, specifically kubernetesVersion, cni, and providers. nodesAndRoles is only needed for the TestProvisioningDynamicInput test, node pools are divided by "{nodepool},". nodeProviders is only needed for node provider cluster tests; the framework only supports custom clusters through aws/ec2 instances.

```json
"provisioningInput": {
    "nodesAndRoles": [ 
      {
        "etcd": true,
        "controlplane": true,
        "worker": true,
        "quantity": 1,
      },
      {
        "worker": true,
        "quantity": 2,
      }
    ],
    "kubernetesVersion": ["v1.24.2-rancher1-1"],
    "providers": ["linode", "aws", "azure", "harvester"],
    "nodeProviders": ["ec2"]
  }
```

### AWS/EC2 Config
For custom clusters, the below config is needed, only AWS/EC2. It is important to note that you MUST use an AMI that already has Docker installed and the service is enabled on boot; otherwise, this will not work.

```json
 "awsEC2Config": {
    "region": "us-east-2",
    "instanceType": "t3a.medium",
    "awsRegionAZ": "",
    "awsAMI": "",
    "awsSecurityGroups": [""],
    "awsAccessKeyID": "",
    "awsSecretAccessKey": "",
    "awsSSHKeyName": "",
    "awsCICDInstanceTag": "",
    "awsIAMProfile": "",
    "awsUser": "ubuntu",
    "volumeSize": 50
  },
```

## Node Template Configs
RKE1 specifically needs a node template config to run properly. These are the inputs needed for the different node providers.

### AWS
```json
  "awsNodeTemplate": {
    "accessKey": "",
    "ami": "",
    "blockDurationMinutes": "0",
    "encryptEbsVolume": false,
    "endpoint": "",
    "httpEndpoint": "enabled",
    "httpTokens": "optional",
    "iamInstanceProfile": "EngineeringUsersUS",
    "insecureTransport": false,
    "instanceType": "t2.2xlarge",
    "keypairName": "jenkins-rke-validation",
    "kmsKey": "",
    "monitoring": false,
    "privateAddressOnly": false,
    "region": "us-east-2",
    "requestSpotInstance": true,
    "retries": "5",
    "rootSize": "16",
    "secretKey": "",
    "securityGroup": ["open-all"],
    "securityGroupReadonly": false,
    "sessionToken": "",
    "spotPrice": "0.50",
    "sshKeyContents": "",
    "sshUser": "ec2-user",
    "subnetId": "subnet-ee8cac86",
    "tags": "",
    "type": "amazonec2Config",
    "useEbsOptimizedInstance": false,
    "usePrivateAddress": false,
    "userdata": "",
    "volumeType": "gp2",
    "vpcId": "vpc-bfccf4d7",
    "zone": "a"
  }
```

### Azure
```json
  "azureNodeTemplate": {
    "availabilitySet": "docker-machine",
    "clientId": "",
    "clientSecret": "",
    "customData": "",
    "diskSize": "30",
    "dns": "",
    "dockerPort": "2376",
    "environment": "AzurePublicCloud",
    "faultDomainCount": "3",
    "image": "canonical:UbuntuServer:18.04-LTS:latest",
    "location": "eastus2",
    "managedDisks": false,
    "noPublicIp": false,
    "openPort": [
      "6443/tcp",
      "2379/tcp",
      "2380/tcp",
      "8472/udp",
      "4789/udp",
      "9796/tcp",
      "10256/tcp",
      "10250/tcp",
      "10251/tcp",
      "10252/tcp"
    ],
    "plan": "",
    "privateIpAddress": "",
    "resourceGroup": "",
    "size": "Standard_D2_v2",
    "sshUser": "azureuser",
    "staticPublicIp": false,
    "storageType": "Standard_LRS",
    "subnet": "docker-machine",
    "subnetPrefix": "192.168.0.0/16",
    "subscriptionId": "",
    "tenantId": "",
    "type": "azureConfig",
    "updateDomainCount": "5",
    "vnet": "docker-machine-vnet"
}
```

### Harvester
```json
"harvesterNodeTemplate": {
    "cloudConfig": "",
    "clusterId": "",
    "clusterType": "",
    "cpuCount": "2",
    "diskBus": "virtio",
    "diskSize": "40",
    "imageName": "default/image-gchq8",
    "keyPairName": "",
    "kubeconfigContent": "",
    "memorySize": "4",
    "networkData": "",
    "networkModel": "virtio",
    "networkName": "",
    "networkType": "dhcp",
    "sshPassword": "",
    "sshPort": "22",
    "sshPrivateKeyPath": "",
    "sshUser": "ubuntu",
    "type": "harvesterConfig",
    "userData": "",
    "vmAffinity": "",
    "vmNamespace": "default"
}
```

### Linode
```json
"linodeNodeTemplate:" { 
    "authorizedUsers": "",
    "createPrivateIp": true,
    "dockerPort": "2376",
    "image": "linode/ubuntu20.04",
    "instanceType": "g6-dedicated-8",
    "label": "",
    "region": "us-east",
    "rootPass": "",
    "sshPort": "22",
    "sshUser": "root",
    "stackscript": "",
    "stackscriptData": "",
    "swapSize": "512",
    "tags": "",
    "token": "",
    "type": "linodeConfig",
    "uaPrefix": "Rancher",
}
```

## RKE2 Provisioning Configs

---

### Provisioning Input
provisioningInput is needed to the run the RKE2 tests, specifically kubernetesVersion, cni, and providers. nodesAndRoles is only needed for the TestProvisioningDynamicInput test, node pools are divided by "{nodepool},". nodeProviders is only needed for node provider cluster tests; the framework only supports custom clusters through aws/ec2 instances.

```json
"provisioningInput": {
    "nodesAndRoles": [
      {
        "etcd": true,
        "controlplane": true,
        "worker": true,
        "quantity": 1,
      },
      {
        "worker": true,
        "quantity": 2,
      }
    ],
    "kubernetesVersion": ["v1.21.6+rke2r1"],
    "cni": ["calico"],
    "providers": ["linode", "aws", "do", "harvester"],
    "nodeProviders": ["ec2"]
  }
```

### AWS/EC2 Config
For custom clusters, the below config is needed, only AWS/EC2 will work.

```json
 "awsEC2Config": {
    "region": "us-east-2",
    "instanceType": "t3a.medium",
    "awsRegionAZ": "",
    "awsAMI": "",
    "awsSecurityGroups": [""],
    "awsAccessKeyID": "",
    "awsSecretAccessKey": "",
    "awsSSHKeyName": "",
    "awsCICDInstanceTag": "",
    "awsIAMProfile": "",
    "awsUser": "ubuntu",
    "volumeSize": 50
  },
```

### Cloud Credentials
These are the inputs needed for the different node provider cloud credentials, inlcuding linode, aws, digital ocean, harvester, azure, and google.

#### Digital Ocean
```json
"digitalOceanCredentials": {
   "accessToken": ""
  },
```
#### Linode
```json
"linodeCredentials": {
   "token": ""
  },
```
#### Azure
```json
"azureCredentials": {
   "clientId": "",
   "clientSecret": "",
     "subscriptionId": "",
     "environment": "AzurePublicCloud"
  },
```
#### AWS
```json
"awsCredentials": {
   "secretKey": "",
   "accessKey": "",
   "defaultRegion": ""
  },
```
#### Harvester
```json
"harvesterCredentials": {
   "clusterId": "",
   "clusterType": "",
   "kubeconfigContent": ""
},
```
#### Google
```json
"googleCredentials": {
    "authEncodedJson": ""
}
```
### Machine RKE Config
Machine RKE pool config is the last thing need for the RKE2 provisioning tests

#### AWS RKE Machine Config
```json
"awsMachineConfig": {
    "region": "us-east-2",
    "ami": "",
    "instanceType": "t3a.medium",
    "sshUser": "ubuntu",
    "vpcId": "",
    "volumeType": "gp2",
    "zone": "a",
    "retries": "5",
    "rootSize": "16",
    "securityGroup": ["rancher-nodes"]
},
```
#### Digital Ocean RKE Machine Config
```json
"doMachineConfig": {
  "image": "ubuntu-20-04-x64",
    "backups": false,
    "ipv6": false,
    "monitoring": false,
    "privateNetworking": false,
    "region": "nyc3",
    "size": "s-2vcpu-4gb",
    "sshKeyContents": "",
    "sshKeyFingerprint": "",
    "sshPort": "22",
    "sshUser": "root",
    "tags": "",
    "userdata": ""
},
```
#### Linode RKE Machine Config
```json
"linodeMachineConfig": {
  "authorizedUsers": "",
  "createPrivateIp": false,
  "dockerPort": "2376",
  "image": "linode/ubuntu20.04",
  "instanceType": "g6-standard-2",
  "region": "us-west",
  "rootPass": "",
  "sshPort": "22",
  "sshUser": "",
  "stackscript": "",
  "stackscriptData": "",
  "swapSize": "512",
  "tags": "",
  "uaPrefix": ""
},
```
#### Azure RKE Machine Config
```json
"azureMachineConfig": {
  "availabilitySet": "docker-machine",
  "diskSize": "30",
  "environment": "AzurePublicCloud",
  "faultDomainCount": "3",
  "image": "canonical:UbuntuServer:18.04-LTS:latest",
  "location": "westus",
  "managedDisks": false,
  "noPublicIp": false,
  "nsg": "",
  "openPort": ["6443/tcp", "2379/tcp", "2380/tcp", "8472/udp", "4789/udp", "9796/tcp", "10256/tcp", "10250/tcp", "10251/tcp", "10252/tcp"],
  "resourceGroup": "docker-machine",
  "size": "Standard_D2_v2",
  "sshUser": "docker-user",
  "staticPublicIp": false,
  "storageType": "Standard_LRS",
  "subnet": "docker-machine",
  "subnetPrefix": "192.168.0.0/16",
  "updateDomainCount": "5",
  "usePrivateIp": false,
  "vnet": "docker-machine-vnet"
},
```
#### Harvester RKE Machine Config
```json
"harvesterMachineConfig": {
  "diskSize": "40",
  "cpuCount": "2",
  "memorySize": "8",
  "networkName": "default/ctw-network-1",
  "imageName": "default/image-rpj98",
  "vmNamespace": "default",
  "sshUser": "ubuntu",
  "diskBus": "virtio"
}
```
## Hosted Provider Provisioning Configs
Below are example configs needed for the different hosted providers including GKE, AKS, and EKS. In order to run these tests, the [cloud credentials](#cloud-credentials) are also needed. GKE (googleCredentials), AKS(azureCredentials), and EKS(awsCredentials)

### EKS Cluster Config
```json
"eksClusterConfig": {
  "imported": false,
  "kmsKey": "",
  "kubernetesVersion": "1.21",
  "loggingTypes": [],
  "nodeGroups": [
    {
      "desiredSize": 2,
      "diskSize": 20,
      "ec2SshKey": "",
      "gpu": false,
      "imageId": "",
      "instanceType": "t3.medium",
      "labels": {},
      "maxSize": 2,
      "minSize": 2,
      "nodegroupName": "",
      "requestSpotInstances": false,
      "resourceTags": {},
      "subnets": [],
      "tags": {}

    }
  ],
  "privateAccess": true,
  "publicAccess": true,
  "publicAccessSources": [],
  "region": "us-east-2",
  "secretsEncryption": false,
  "securityGroups": [""],
  "serviceRole": "",
  "subnets": ["", ""],
  "tags": {}
},
```
### AKS Cluster Config
```json
"aksClusterConfig": {
  "dnsPrefix": "-dns",
  "imported": false,
  "kubernetesVersion": "1.21.9",
  "linuxAdminUsername": "azureuser",
  "loadBalancerSku": "Standard",
  "networkPlugin": "kubenet",
  "nodePools": [
    {
      "availabilityZones": ["1", "2", "3"],
      "nodeCount": 1,
      "enableAutoScaling": false,
      "maxPods": 110,
      "mode": "System",
      "name": "agentpool",
      "osDiskSizeGB": 128,
      "osDiskType": "Managed",
      "osType": "Linux",
      "vmSize": "Standard_DS2_v2"
    }
  ],
  "privateCluster": false,
  "resourceGroup": "",
  "resourceLocation": "eastus",
  "tags": {}
},
```
### GKE Cluster Config
```json
"gkeClusterConfig" : {
  "clusterAddons": {
    "horizontalPodAutoscaling": true, 
    "httpLoadBalancing": true, 
    "networkPolicyConfig": false
  },
  "horizontalPodAutoscaling": true,
  "httpLoadBalancing": true,
  "networkPolicyConfig": false,
  "clusterIpv4Cidr": "",
  "enableKubernetesAlpha": false,
  "ipAllocationPolicy": {
    "clusterIpv4Cidr": "",
    "clusterIpv4CidrBlock": null,
    "clusterSecondaryRangeName": null,
    "createSubnetwork": false,
    "nodeIpv4CidrBlock": null,
    "servicesIpv4CidrBlock": null,
    "servicesSecondaryRangeName": null,
    "subnetworkName": null,
    "useIpAliases": true
  },
  "kubernetesVersion": "1.21.9-gke.1002",
  "labels": {},
  "locations": [],
  "loggingService": "logging.googleapis.com/kubernetes",
  "maintenanceWindow": "",
  "masterAuthorizedNetworks": {
    "enabled": false
  },
  "monitoringService": "monitoring.googleapis.com/kubernetes",
  "network": "default",
  "networkPolicyEnabled": false,
  "nodePools": [
    {
      "autoscaling": {
        "enabled": false,
        "maxNodeCount": null,
        "minNodeCount": null
      },
      "config": {
        "diskSizeGb": 100,
        "diskType": "pd-standard",
        "imageType": "COS",
        "labels": {},
        "localSsdCount": 0,
        "machineType": "n1-standard-2",
        "oauthScopes": [
          "https://www.googleapis.com/auth/devstorage.read_only",
          "https://www.googleapis.com/auth/logging.write",
          "https://www.googleapis.com/auth/monitoring",
          "https://www.googleapis.com/auth/servicecontrol",
          "https://www.googleapis.com/auth/service.management.readonly",
          "https://www.googleapis.com/auth/trace.append"
        ],
        "preemptible": false,
        "tags": null,
        "taints": null
      },
      "initialNodeCount": 3,
      "isNew": true,
      "management": {
        "autoRepair": true, 
        "autoUpgrade": true
      },
      "maxPodsConstraint": 110,
      "name": ""
    }
  ],
  "privateClusterConfig": {
    "enablePrivateEndpoint": false, 
    "enablePrivateNodes": false, 
    "masterIpv4CidrBlock": null
  },
  "projectID": "",
  "region": "",
  "subnetwork": "default",
  "zone": "us-central1-c"
}
```