# Robert is getting to know RH Openshift

- Installed it using the [Assisted Installer](https://docs.openshift.com/container-platform/4.15/installing/installing_vsphere/installing-vsphere-assisted-installer.html) via the RH [Hybrid Cloud Console](https://console.redhat.com/)
  - Created an iso for the base-installation using the following [guidance](https://access.redhat.com/documentation/en-us/assisted_installer_for_openshift_container_platform/2024/html/installing_openshift_container_platform_with_the_assisted_installer/installing-on-vsphere)
  - Created three VMs á 8 vCPUs, 32GB RAM and 120 GB Disk
  - Connected to a DHCP enabled network
  - reserved a static IP for the Kubernetes cluster API `api.rguske-os-cl1.cpod-nsxv8.az-stc.cloud-garage.net`
  - created a wildcard DNS entry for Ingress `*.apps.rguske-os-cl1.cpod-nsxv8.az-stc.cloud-garage.net`
  - Configured the virtual machines with the advanced parameters `disk.EnableUUID`
- Powered.on all three vms and used the auto-discovery feature in the Hybrid Cloud Console
  - Selected the type `Control-Plane` and continued the wizard
- Downloaded the `oc` CLI:

```bash
 wget https://mirror.openshift.com/pub/openshift-v4/x86_64/clients/ocp/stable/openshift-client-linux.tar.gz
--2024-05-22 14:09:20--  https://mirror.openshift.com/pub/openshift-v4/x86_64/clients/ocp/stable/openshift-client-linux.tar.gz
Resolving mirror.openshift.com (mirror.openshift.com)... 18.66.27.44, 18.66.27.34, 18.66.27.89, ...
Connecting to mirror.openshift.com (mirror.openshift.com)|18.66.27.44|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 65427837 (62M) [application/x-tar]
Saving to: ‘openshift-client-linux.tar.gz’

openshift-client-linux.tar.gz                           100%[============================================================================================================================>]  62,40M  23,5MB/s    in 2,7s    

2024-05-22 14:09:23 (23,5 MB/s) - ‘openshift-client-linux.tar.gz’ saved [65427837/65427837]
```

- Obtained the access-token via `oc login https://api.rguske-os-cl1.cpod-nsxv8.az-stc.cloud-garage.net:6443`
  - validated login

## Create first Openshift Cluster