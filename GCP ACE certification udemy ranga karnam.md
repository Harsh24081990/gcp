# SECTION-4
## Keeping the compute cost low 
### 1. Sustained use discounts 
- Automatic discounts for running VM more than 20% of the month.
- applicable for instances created by GKE and compute engines. 
- NOT  applicable for instances created by App Engine flexible and Dataflow. 
- NOT  applied on certain types of VMs (Ex. E2, A2)

### 2. Committed use discounts
- for predictable resources need.
- commit for 1 year or 3 year.
- discounts are higher than sutained use discount.
- appliable for -- GKE and compute engine instances.
- NOT  applicable for instances created by App Engine flexible and Dataflow. 
- Goto --> Compute Engine -- committed use discounts -- PURCHASE COMMITMENT.

### 3. Use Preemptible VM
- short lived (24 hours) cheaper (upto 80% cheaper)
- can be stopped by google with a 30 second warning to save the work.
- can use if our apps are
      - fault tolerant
      - cost sensitive
      - non critical. 
- can NOT migrated to regular VMs and NO SLA is guranteed. 
- No restart available.
--> while creating VM --> go to Availability policy -- "on" the preempitible VM. 

### 4. Spot VMs : Latest version of the preemptible VM.
difference --> Done not have max run time of 24 hours which is there in case of preemptible VMs. 
other than this every thing is same. 

-----------------------------------------------------------------

# Billing for GCE VMs
- minimum billed for 1 min.
- after that billed by the second. 
- attached storages are keep on billing.
- create "Budgets & alerts" -- Set alert threshould rule.
-------------------------------------------------------------

# Achieving high availability with live migration and automatic restart.
- Live Migration : running instance is migratied to another host in the same zone. 
- not supported for GPUs and reemptible instances (spot).
- Configure *`Availability Policy`*
set *`On host maintenance`* 
and *Automatic restart*
-------------------------------------------------------------

# custom machine types:
we can choose the CPU, memory, OS etc. 
- we can choose between the E2, N2 and N1 machine types. 
--------------------------------------------------------------
# GPU in GCE
For graphical and math intensive workload. 
- Choose Machine Family as "GPU" while creating the VM. 
or Add GPU in Gernal purpose Machine family. 
---------------------------------------------------------
# Virtual Machine - Review
- a VM is Associated with a project. 
- machine type availabilty can vary from region to regions. 
- must need to stop the VM to change (EDIT) the machine type (adjust the cpu/memory etc.). 
- Instances are Zonal and Regional 
- but the images are global.
- by default instance template are also global until we have created a zonal template. 
- In VM, basic monitoring is enabled by default (CPU utilization, Network bytes, disk throughput/IOPS)
- For memory utilization & Disk space utilization, cloud monitoring agent is needed. 
---------------------------------------------------------------

# VM - best prctices
- choose the right zone and right region based on:
cost, regulations, latency and specifi hardware needs. as near as possible to users. 
- distribute instances in multiple zone and regions for high availability. 
--> Righ machine type :
- math/graphich --GPU
- constant workload --use "committed use discounts"
--> Add labels to indicate env, team, business units etc.
---------------------------------------------------------
# Compute Engine Scenarios:
=> Pre-requisites to create VM:
1. Projects, 2. billing account, 3. compute engine API should be enabled.

=> If Need dedicated hardware for your compliance, licensing and management:
go to Compute ENgine -->select *Sole-tenant node*
- create a node template.
- add some Affinity lables. This can be used to create more VM in the same node. 

=> Automatic OS patch, OS inventory management and OS configuration management (manage software installed on 1000s of VMs.) 
- Compute Engine --> VM Manager --> OS patch management. 

==> don't want to expose VM to internet
- Don't assign a public IP. 
------------------------------------------------------------

# Quick Review
- Image
- Custom image
- Machine Types
- Static IP address. 
- Instance Templates. 
- sustained use discounts.
- committed use discounts. 
- preemptible VM
- spot instance. 
-------------------------------------------------------------
# SECTION-5
## Gclod
command line interface to interact with GC resources and services. It's a part of GC SDK. requres python. 
- need to install cloud SDK to if need to use gcloud on our local macine. 
- some GCP services have specific CLI tool such as::
    - storage - gsutil
    - big query - bq
    - bigtable - bct
    - kubernetes - kubectl

=> cloud shell : place to run gcloud commands (in portal itself. no need to install cloud SDK)
--> gcloud --version
--> gcloud init
------------------------------------------------------------------------
## Manage multiple config using gcloud.
--> gcloud config configuration list
using this command we can see the different configs currently available. which shows config name, project names, region,  zones etc details. 

--> gclould config configurations create <confiname>

--> gcloud config set project <project-name>

--> gclould config list project

- How to switch config ?
--> gcloud config configurations activate <configname>

- How to discribe config?
--> gcloud config configuraiton describe <configname>

--> gclould config configration create/delete/describe/activate/list

----------------------------------------------------

## gcloud command structure
gcloud GROUP SUBGROUP ACTION...
=> GROUP -->config/compute/container/dataflow/functions/IAM/...
=> SUBGROUP -->instances/images/instance template/ machine types/ regions/ zones
=> ACTION --> create/list/start/stop/describe/delte.

Examples: -

--> gcloud compute instances list
--> gcloud compute instances create <my-instance-name>
--> gcloud compute instances describe <my-instance-name>
--> gcloud compute instances delete <my-instance-name>
--> gcloud compute instances list
--> gcoud compute zones list
--> gcoud compute regions list
--> gcoud compute machine-types list
--> gcoud compute machine-types list --filter zone:asia-southeast2-b
--> gcoud compute machine-types list --filter "zone:(asia-southeast2-b asia-southeast2-c)"
--------------------------------------------------------

# gcloud compute instance create various options.

--> gcloud compute machine-types list
--> --custome-cpu
--> --image or --image family
--> --zones
--> --tags
--

------------------------------------------------------






