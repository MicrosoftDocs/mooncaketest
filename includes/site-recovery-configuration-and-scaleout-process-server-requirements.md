| **Hardware** | |
| --- |---|
| Number of CPU cores| 8 |
| RAM| 12 GB|
| Number of disks | 3 <br><br> - OS disk<br> - Process server cache disk<br> - Retention drive (for failback)|
| Disk free space (process server cache) | 600 GB
| Disk free space (retention disk) | 600 GB|
| **Software** | |
| Operating system version | Windows Server 2012 R2 |
| Operating system locale | English (en-us)|
| VMware vSphere PowerCLI version | [PowerCLI 6.0](https://developercenter.vmware.com/tool/vsphere_powercli/6.0 "PowerCLI 6.0")|
| Windows Server roles | Do not enable the following roles: <br> - Active Directory Domain Services <br>- Internet Information Services <br> - Hyper-V |
| **Network** | |
| Network interface card type | VMXNET3 |
| IP address type | Static |
| Internet access | The server should be able to access the following URLs either directly or through a proxy server: <br> - \*.accesscontrol.chinacloudapi.cn<br> - \*.backup.windowsazure.cn <br>- \*.store.core.chinacloudapi.cn<br> - \*.blob.core.chinacloudapi.cn<br> - \*.hypervrecoverymanager.windowsazure.cn <br>  |
| Ports | 443 (Control channel orchestration)<br>9443 (Data transport)|