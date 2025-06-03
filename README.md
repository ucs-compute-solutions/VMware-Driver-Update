# Install or Upgrade VMware Drivers

Note that the scripts in this repository have now been successfully tested with VMware vSphere 8.0 Update 3.

This repository for FlexPod contains an Ansible playbook to install and upgrade VMware drivers for Cisco UCS nenic and nfnic, Cisco UCS Tool to report to Intersight, Cisco UCS storage drivers if necessary, and the NetApp NFS VAAI plugin if necessary.

# Set up the execution environment

To execute this ansible playbook, a linux based system (RHEL 9 and Rocky Linux 9 have been tested) will need to be setup. Install default Server with GUI and add XRDP and Visual Studio Code. Then execute the following steps from a user home directory:
1. sudo dnf install python3.11
2. curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
3. python3.11 get-pip.py
4. rm get-pip.py
5. python3.11 -m pip install --user ansible
6. echo [defaults] > ~/.ansible.cfg
7. echo interpreter_python=/usr/bin/python3.11 >> ~/.ansible.cfg
8. ansible --version
9. sudo dnf install git

# How to execute this playbook?

1.  Create a directory and clone the repository from Github with "git clone https://github.com/ucs-compute-solutions/VMware-Driver-Update.git".
2.  Check the Cisco UCS HCL selecting your server type and VMware version at https://ucshcltool.cloudapps.cisco.com/public/#. Checking against the listing for the exact version of VMware ESXi your are installing from the Broadcom Support site, determine the drivers needed for the version of server firmware that you plan to run.
3.  Download the needed drivers from Cisco via server VMware driver ISOs and the UCS vSphere Installation bundle and the NetApp NFS VAAI plugin if necessary and place on an http: (not https:) server.
4.  Fill in all of the variable files in the playbook. You need to determine if you will upgrade the drivers on your servers one at a time with Maintenance Mode and reboot or just upgrade the drivers on all the servers then put each server in Maintenance Mode and reboot in sequence. Fill in the inventory file accordingly.
5.  Execute the playbook with "ansible-playbook ./Install_ESXi_Drivers.yml -i inventory" to install or update the drivers.
