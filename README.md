[![published](https://static.production.devnetcloud.com/codeexchange/assets/images/devnet-published.svg)](https://developer.cisco.com/codeexchange/github/repo/ucs-compute-solutions/FlexPod-IMM-VMware)

# Install or Upgrade VMware Drivers

Note that the scripts in this repository have now been successfully tested with VMware vSphere 8.0 Update 3.

This repository for FlexPod contains an Ansible playbook to install and upgrade VMware drivers for Cisco UCS nenic and nfnic, Cisco UCS Tool to report to Intersight, Cisco UCS storage drivers if necessary, and the NetApp NFS VAAI plugin.

# Set up the execution environment

To execute various ansible playbooks, a linux based system will need to be setup as described in the https://www.cisco.com/c/en/us/td/docs/unified_computing/ucs/UCS_CVDs/flexpod_base_imm_m7_iac.html CVD with the packages listed at the following pages:

- Cisco UCS Intersight: https://galaxy.ansible.com/ui/repo/published/cisco/intersight/
- Cisco NxOS: https://galaxy.ansible.com/ui/repo/published/cisco/nxos/
- NetApp ONTAP: https://galaxy.ansible.com/ui/repo/published/netapp/ontap/
- VMware: https://galaxy.ansible.com/ui/repo/published/community/vmware/

# How to execute this playbooks?

1.  Create a directory and clone the repository from Github with "git clone https://github.com/ucs-compute-solutions/FlexPod-IMM-VMware.git".
2.  Check the Cisco UCS HCL selecting your server type and VMware ESXi 8.0U3 at https://ucshcltool.cloudapps.cisco.com/public/#. Checking against the listing for the exact version of VMware ESXi your are installing from the Broadcom Support site, determine the drivers needed for the version of server firmware that you plan to run.
3.  Download the needed drivers from Broadcom and the NetApp NFS VAAI plugin and place on an http: (not https:) server.
4.  Fill in all of the variable files in the playbook. You need to determine if you will upgrade the drivers on your servers one at a time with Maintenance Mode and reboot or just upgrade the drivers on all the servers then put each server in Maintenance Mode and reboot in sequence. Fill in the inventory file accordingly.
5.  Execute the playbook with "ansible-playbook ./Install_ESXi_Drivers.yml -i inventory" to install or update the drivers.