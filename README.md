## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![diagram](https://raw.githubusercontent.com/peteypipe/Cloud-deployment-in-azure/main/azure%20with%20elk.JPG
)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select portions of the project may be used to install only certain pieces of it, such as Filebeat.

  [Ansible build files](https://github.com/peteypipe/Cloud-deployment-in-azure/tree/main/azureuser/ansible)
  

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient, in addition to restricting downtime in the network.
- Load balancers provide a level of security in their ability to protect against DDoS attacks by spreading the traffic between mutliple servers. They provide a layer of redundancy to a network by connecting to several servers at one time and allowing for servers to be taken down or added without disrupting user access. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system files.

- filebeat monitors and centralizes log data and forwards data that you specify for indexing. 

- Metricbeat records metrics for the OS and services running on the server that it is monitoring. 

The configuration details of each machine may be found below.


| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| WEB 1    | DVMA     | 10.0.0.5   | Linux            |
| WEB 2    | DVMA     | 10.0.0.6   | Linux            |
| ELK      | MONITOR  | 10.1.0.4   | Linux            |
| LoadBalance| Traffic| 168.61.213.189| Linux 
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Host machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 40.122.44.25


Machines within the network can only be accessed by the JumpBox.
- The elk VM is only accessible via the JumpBox (10.0.0.4) and then the docker container. Once connected to the docker container, users can ssh into the elk vm. 

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 40.122.44.25         |
| Web 1    | No                  | 10.0.0.4             |
| Web 2    | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because the playbook can be used to configure multiple servers in the same manner. 

The playbook implements the following tasks:
-
- Configuring the memory and setting it to the a specific paramter for operation
- download docker.io 
- install python-3 and python module

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![](https://raw.githubusercontent.com/peteypipe/Cloud-deployment-in-azure/main/docker%20ps.JPG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
-Web-1 10.0.0.5
-Web-2 10.0.0.6

We have installed the following Beats on these machines:
-Filebeat
-Metricbeat

These Beats allow us to collect the following information from each machine:

- Filebeat is collecting and centralizing log data that is specified by the user which is then shipped for indexing. Metricbeat tracks the 'metrics' of the OS and services running on a server that it is monitoring. 
- E.X filebeat
  agent.hostname:web-1 agent.id:e53fbdde-8724-4351-a5a7-b71d97e02d28 agent.type:filebeat agent.ephemeral_id:67ab21d4-c541-4df9-91d0-e9340ba30f12 agent.version:7.6.1 process.name:metricbeat process.pid:708 log.file.path:/var/log/syslog log.offset:1,232,352 fileset.name:syslog message:2021-12-26T22:11:22.358Z#011INFO#011[monitoring]#011log/log.go:145#011Non-zero metrics in the last 30s#011{"monitoring": {"metrics": {"beat":{"cpu":{"system":{"ticks":42320,"time":{"ms":80}},"total":{"ticks":108110,"time":{"ms":258},"value":108110},"user":{"ticks":65790,"time":{"ms":178}}},"handles":{"limit":{"hard":524288,"soft":1024},"open":15},"info":{"ephemeral_id":"002b4a2f-e254-4e99-a1dc-c3b71099a513","uptime":{"ms":12902281}},"memstats":{"gc_next":15040112,"memory_alloc":8564184,"memory_total":16930183880},"runtime":{"goroutines":67}},"libbeat":{"config":{"module":{"running":0}},"output":{"events":{"acked":67,"batches":9,"total":67},"read":{"bytes":3561},"write":{"bytes":123356}},"pipeline":{"clients":4,"events":{"active":0,"published":67,"total":67},"queue":{"acked":67}}},"metricbeat":{"docker":{"container":{"events":3,"success":3},"cpu":{"events":3,"success":3},"diskio"
-E.x metricbeat
  @timestamp:Dec 26, 2021 @ 17:36:36.182 docker.info.id:OBLG:ILDC:F3DK:NZNB:LL6W:5SB2:7MC4:GR7J:BPKW:EGE5:SLDI:KAJF docker.info.containers.stopped:0 docker.info.containers.total:1 docker.info.containers.running:1 docker.info.containers.paused:0 docker.info.images:1 event.dataset:docker.info event.module:docker event.duration:8.5 ecs.version:1.4.0 host.os.platform:ubuntu host.os.version:20.04.3 LTS (Focal Fossa) host.os.family:debian host.os.name:Ubuntu host.os.kernel:5.11.0-1022-azure host.os.codename:focal host.id:2fb28d878c40430baf3a609c446df6bb host.containerized:false host.name:web-1 host.hostname:web-1 host.architecture:x86_64 agent.type:metricbeat agent.ephemeral_id:002b4a2f-e254-4e99-a1dc-c3b71099a513 agent.hostname:web-1 agent.id:ddc705f3-016b-4dbb-9f08-ff275b57c685 agent.version:7.6.1 cloud.machine.type:Standard_B1ms cloud.region:centralus cloud.instance.id:effdefd9-44ad-433d-9d26-a343e4e10d8a cloud.instance.name:web-1 cloud.provider:az metricset.period:10,000 metricset.name:info service.type:docker service.address:/var/run/docker.sock _id:fk4a-X0BlvIxNHJiaFA6 _type:_doc _index:metricbeat-7.6.1-2021.12.17-000001 _score: -
  

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the __host__ file to __the environment___.
- Update the ___host__ file to include the correct group and IP address's 
- Run the playbook, and navigate to __kibana__ to check that the installation worked as expected.


