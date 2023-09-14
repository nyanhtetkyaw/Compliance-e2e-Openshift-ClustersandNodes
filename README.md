### Managing Compliance e2e Openshift Clusters and Nodes


**Installing and Configuring OpenShift Local**

1. Start by installing the CentOS-8-Stream operating system on your system. You can download the ISO image from the CentOS website and follow the installation process. Below link is the reference to install the CentOS installation. 
https://www.server-world.info/en/note?os=CentOS_8&p=install

_Hardware requirements_
Processor: Minimum 2 
RAM: Minimum 16GB 
Disk: Minimum 120GB

2. Execute the following commands after CentOS installation  To grant user sudo privileges, execute the below command:

echo ‘osl ALL=(ALL) NOPASSWD:ALL’ >> /etc/sudoers.d/osl 
This allows osl to execute commands with administrative privileges.

3. Open the NetworkManager Text User Interface (nmtui):  
The command nmtui opens the NetworkManager TUI, which provides an interactive interface to manage network connections on CentOS. Select the interface to enable auto connect.

4. Create a “bin” directory:  
Use the command mkdir bin to create a directory named “bin” in the home directory.

5. Add bin directory to the PATH: To add the “bin” directory to the PATH environment variable, execute the below command:

export PATH=$PATH:$HOME/bin.

Additionally, you can add this command to the .bashrc file to ensure the PATH modification persists across sessions by executing below command:
echo ‘export PATH=$PATH:$HOME/bin’ >> ~/.bashrc.

6. Move crc and oc installer to the ~/bin/ directory

**Setup and Installation of OpenShift Local**

1. Check the CRC version  Open a terminal and execute the command crc version to check the version of CRC installed on your system. This command displays the version information of the CRC tool.

2. Delete any existing CRC instance  Execute the command crc delete to remove any existing CRC instance from your system. This step ensures a clean installation.

3. Set the consent telemetry to “no”  Use the command crc config set consent-telemetry no to disable telemetry consent for CRC. This step ensures that telemetry data is not sent to the OpenShift developers.

4. Set the CRC preset to “openshift”  Execute the command crc config set preset openshift to set the CRC preset to “openshift” for installation. This preset ensures that the OpenShift cluster is configured with the appropriate settings.

5. Set up CRC  Run the command crc setup or setup with crc bundle crc setup -b <bundle> to set up CRC on your system. This command downloads the necessary files and sets up the CRC environment.    
CRC Bundles

Windows
crc setup -b https://storage.googleapis.com/crc-bundle-github-ci/4.12.5/crc_hyperv_4.12.5_amd64.crcbundle

Linux
crc setup -b https://storage.googleapis.com/crc-bundle-github-ci/4.12.5/crc_libvirt_4.12.5_amd64.crcbundle

Mac-Intel
crc setup -b https://storage.googleapis.com/crc-bundle-github-ci/4.12.5/crc_vfkit_4.12.5_amd64.crcbundle

Mac-M1
crc setup -b https://storage.googleapis.com/crc-bundle-github-ci/4.12.5/crc_vfkit_4.12.5_arm64.crcbundle

Note: must be enable virtual hypervisor before you start the VM  Enable with below command if you are using on the esxi

#> find / -name *.vmx |grep Open

#> echo ‘vhv.enable = “TRUE” >> /vmfs/volumes/628ebe24–088f8b46–1a1f-6c0b84e0d61e/Openshift-local/Openshift-local.vmx

![Show All](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/44cc30c7-e842-47a4-beb7-7dbc291dddf9)
![1RoI4HGpgULAhiKjrx9M0aQ](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/97d51eab-6cfd-44a9-9ae6-fb101521fe86)

Download local installer

![11dBumifiyifGs5wewxq_NQ](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/494d55a4-9374-4023-b4cb-8e4016790902)

6. Start the CRC instance  Execute the command crc start to start the CRC instance. If you have a pull secret, you can provide it using the command 'crc start -p pull-secret.txt' replacing “pull-secret.txt” with the path to your pull secret file. Starting the CRC instance provisions a local OpenShift cluster.

![1e_hKNT4fPzKv-VAwSRcZzQ](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/cb391353-0904-4200-a04b-117373d23867)
![etcNetworkManagerdnsmasq dcrc conf exists](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/f021ebda-d5e2-435d-8d3a-5861fb9bed5b)
![Started the Openshift cluster](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/35117b11-c887-4bf2-a700-12766e8ef553)

7. Access the OpenShift console and obtain credentials  Use the command 'crc console'
credentials to display the credentials for accessing the OpenShift console. These credentials include the username and password required to log in to the OpenShift web console.

![1kC8VHBBiL_-5HWhcrCG_3A](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/6a93ddb2-729f-4ce2-a102-e8d87de0293a)

8. Set the OpenShift environment and context to crc-admin   Use the commands 'crc oc-env' and 'crc config use-context crc-admin' to set the OpenShift context to 'crc-admin' for administrative access. This ensures that subsequent OpenShift commands are executed within the correct context.
9. Verify the user  Execute the command oc whoami to verify the currently logged-in user. This command displays the username associated with the current OpenShift context.

**Installing the OpenShift Compliance Operator**

![Openshift Compliance Operator Declarative Security Compliance](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/9f22e6b7-16d0-43c5-bad5-672b7df2a571)

1. Check OperatorHub for the Compliance Operator  Access the OpenShift web console using the URL displayed in the terminal after starting the CRC instance. Navigate to the “OperatorHub” section and search for the “Compliance Operator” Check if it is available for installation.

2. Install the Compliance Operator From the OperatorHub page, click on the “Compliance Operator” card and then click “Install” Choose the appropriate installation mode and namespace and follow the prompts to complete the installation.

![1Goj257FHrPmv4YkjPOKSdQ](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/220c915a-a55e-43e3-9d11-120b77047a85)
![1_Cd-nmzXYKBkS0MGbVheGw](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/249855ed-4812-4787-95d1-526048ed5787)
![Compliance Operator](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/44cfcc35-a43a-41f7-828a-e7561325368b)
![19EWTeouB4ONF0RCHEBpM9w](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/02602712-24b2-4650-a75e-df7ea7d793ac)
![Compliance Operator](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/e1d56e12-1dfa-4aed-912a-c1172dd71e84)
![Compliance Operator](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/1fa9a40d-8842-4479-9c16-45569d32f2e4)
![Under the hood](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/dc5126e5-8178-4583-bce7-ca39495727a4)
![15moeI99Nw17dcqx2iWGYbw](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/ea53879b-ef4c-44b1-9eb2-c144a9822416)

3. Verify the Compliance Operator installation to use the command 'oc get project' to check the project status of the Compliance Operator. Ensure that the Compliance Operator pods are in the “Running” state.

**Managing Compliance Scans and Reports**

1. Use 'oc get profilebundle.compliance' and 'oc get profile.compliance' to see the compliance valid profiles.

![1L1ZP2qhrmm3qH0Os7799Dw](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/cc56dc9a-ae14-42f7-87a1-ac3a1e2e31cb)

2. Use 'oc get rules.compliance' to see the compliance rules.

![ocp4-alert-receiver-configured](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/ccd9ea54-3f6b-4002-a5f1-66bc8e472c72)

3. Use 'oc get variables.compliance -nopenshift-compliance' to see the variables

![ocp4-hypershift-cluster](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/1cdf80e1-0176-4c69-a33f-1975dddd7881)

4. Get the default scan settings

![kind ScanSetting](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/006cfe72-4011-41fb-8a54-15b0dc62506b)

![effect Noschedule](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/13763514-829b-473e-b988-f0f3e07648ef)

5. Create scansettingbindings  
Below is the example ScanSettingBinding will be using default-auto-apply scansetting script because we want to apply auto, however you can either use the default as well.

Note: Different profilebundle can’t be use together in the same scansettingbindings

![Namespace openshif-compliance](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/135f4d95-3cd1-4a9a-85f3-95e4ae28a190)
![12ntDMQ0uoUCNc--Zs-2RBg](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/805c2025-b6eb-4e24-9593-1a999f3cb64f)

6. Use the command 'oc create -f scansettingbindings.yaml -nopenshift-compliance' to create scansettingbindings using the provided YAML files.
Verifying the Scanning Status to use the command 'oc get compliancescans -nopenshift-compliance' After creating the scansettingbindings, perform the following checks:

![COMPLIANT](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/fe843406-c479-458c-8964-ee8e10e81d4f)

· Rerun the scanning setting with below commands:
oc-compliance rerun-now compliancescan <name>
oc-compliance rerun-now compliancesuite <name>
oc-compliance rerun-now scansettingbindings <name>

· Get the severity filtering with below command:
oc get compliancecheckresult -l compliance.openshift.io/scan-name=ocp4-cis-node,compliance.openshift.io/check-serverity=medium
oc get compliancecheckresults -nopenshift-compliance -lcompliance.openshift.io/check-status=FAIL,compliance.openshift.io/check-serverity=high

· Change Scanning Profiles and Retrieve Information:  
To change the scanning profiles and retrieve information, use the provided commands below:
Edit scansettingbindings to change the profile 'oc edit ssb scansettingbinding -nopenshift-compliance' to edit the scansettingbindings and change the profile.

Get compliance profile information 'oc get profile.compliance -nopenshift-compliance' to retrieve information about compliance profiles.

Get information about persistent volume claims 'oc get pvc -nopenshift-compliance' to get information about persistent volume claims.

Get the profile scan result 'oc get compliancecheckresult -nopenshift-compliance' to get the profile scan result.

![STATUS SEVERITY](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/36d96aab-516e-4df9-9bd1-6c120418de06)

Review the result with below command:
oc-compliance view-result ocp4-cis-node-master-file-owner-kube-apiserver compliancecheckresults -nopenshift-compliance

Count the result with below command: 
echo -n PASS: && oc get compliancecheckresult -n openshift-compliance |grep PASS | wc -l && \
echo -n FAIL: && oc get compliancecheckresult -n openshift-compliance |grep FAIL | wc -l && ;

Manual remediate with the below command:
oc -nopenshift-compliance patch complianceremediations/ ocp4-cis-node-master -sysctl-net-ipv4-conf-all-accept-redirects — patch ‘{“spec”:{“apply”:true}}’ — type=merge

oc -nopenshift-compliance patch complianceremediations/rhcos4-high-master-service-sshd-disabled — patch ‘{“spec”:{“apply”: true}}’ — type=merge

Get the instruction to remediation:
oc get rule ocp4-kubelet-configure-tls-cipher-suites -o=jsonpath={.instructions}

View the content with python script:

echo “net.ipv4.conf.all.accept_redirects%3D0” | python3 -c “import sys, urllib.parse; print(urllib.parse.unquote(‘’.join(sys.stdin.readlines())))”

Get the persistent volumes and pods:

![11VerPW1_x1cKUuG0NfsLLA](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/a0663d12-e719-4648-a153-08e4d94baef2)

**Report Collection and Analysis**

To collect and analyse compliance reports and I selected to using the rhel8 pod, so that we can easy to identify the report location via pod terminal, follow these steps:

![Create Pod](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/f4801dda-4d36-49ea-a1fe-ebca769d675d)

· Create the report-collector pod using the report-collector.yaml file: 
Use 'oc create -f report-collector.yaml -nopenshift-compliance' to create the report-collector pod. In this step can be use pv-extract-pod as well but terminal is not available with this pod, So I choose to use other linux to identify the mount-point before collect.

· Check the status of the collector pod 'oc get pods -nopenshift-compliance' to check the status of the collector pod.

· You can easily identify the report location and mount point on the pod terminal, below is the example steps.

![report-collector-master](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/933f243c-b7d3-4c0a-8498-9bebf53308ee)

· Copy the report from the pod: Use the oc cp command to copy the report from the pod and generate an HTML report using oscap xccdf generate report.

· Copy the report from master node  'oc cp reporter:/reports/1/ocp4-cis-node-master-crc-8cf2w-master-0-pod.xml.bzip2 ./ reportcismaster.bzip2 -nopenshift-compliance'

· Extract the bzip file with below command
· bzip2 -dk reportcismaster.bzip2
· Convert the out file to the report with OpenSCAP
· oscap xccdf generate report reportname.bzip2.out > report.html

![1pSFIVAwkEljWirQOrqQhbg](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/0787e091-7c34-4b2e-bde8-80c0a3711180)
![1YgFebld0xxLjJlUlbqRcDw](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/345e1718-1242-44de-90fe-ce7c6a35871f)
![©) OpenSCAP Evaluation Report](https://github.com/nyanhtetkyaw/Compliance-e2e-Openshift-ClustersandNodes/assets/24841368/990547d2-cbb7-4755-a1cb-19593d8a1d8a)

· Re-execute a compliance: 
To initiate a rescan or update the scans, use the command 'oc annotate compliancescan/ocp4-cis compliance.openshift.io/rescan=<scansettingbinding name> -nopenshift-compliance'

· By following these steps, you can successfully install and configure OpenShift local, install the OpenShift Compliance Operator, and manage compliance scans and reports.

Hope you enjoy the reading…

Reference:

https://www.redhat.com/en/resources/openshift-security-guide-ebook?extIdCarryOver=true
https://cloud.redhat.com/blog/how-does-compliance-operator-work-for-openshift-part-1
https://cloud.redhat.com/blog/how-does-compliance-operator-work-for-openshift-part-2
https://github.com/openshift/compliance-operator
https://github.com/ComplianceAsCode/content
https://docs.openshift.com/container-platform/4.3/authentication/identity_providers/configuring-ldap-identity-provider.html
https://bugzilla.redhat.com/show_bug.cgi?id=2082416
https://bugzilla.redhat.com/show_bug.cgi?id=2032420
http://static.open-scap.org/openscap-1.3/oscap_user_manual.html  

Plans to update Profile Tailoring in the near feature.
