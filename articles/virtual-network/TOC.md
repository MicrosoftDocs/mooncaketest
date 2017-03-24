# 概述
## [虚拟网络](virtual-networks-overview.md)
## [用户定义的路由和 IP 转发](virtual-networks-udr-overview.md)
## [虚拟网络对等互连](virtual-network-peering-overview.md)
## [业务连续性](virtual-network-disaster-recovery-guidance.md)
## [常见问题](virtual-networks-faq.md)
## IP 寻址
### [Resource Manager](virtual-network-ip-addresses-overview-arm.md)
### [经典](virtual-network-ip-addresses-overview-classic.md)
## 虚拟机
### [网络接口](virtual-network-network-interface-overview.md)
### [名称解析](virtual-networks-name-resolution-for-vms-and-role-instances.md)

# 入门
## [创建虚拟网络](virtual-networks-create-vnet-arm-pportal.md)
## [将 VM 部署到虚拟网络](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fmooncaketest%2farticles%2fvirtual-network%2ftoc.json)

# 如何
## 规划和设计
### [虚拟网络](virtual-network-vnet-plan-design-arm.md)
### [网络安全组](virtual-networks-nsg.md)

## 部署
### 虚拟网络
#### [门户](virtual-networks-create-vnet-arm-pportal.md)
#### [PowerShell](virtual-networks-create-vnet-arm-ps.md)
#### [CLI](virtual-networks-create-vnet-arm-cli.md)
#### [模板](virtual-networks-create-vnet-arm-template-click.md)
#### [门户（经典）](virtual-networks-create-vnet-classic-pportal.md)
#### [PowerShell（经典）](virtual-networks-create-vnet-classic-netcfg-ps.md)
#### [CLI（经典）](virtual-networks-create-vnet-classic-cli.md)

### 网络安全组
#### [门户](virtual-networks-create-nsg-arm-pportal.md)
#### [PowerShell](virtual-networks-create-nsg-arm-ps.md)
#### [CLI](virtual-networks-create-nsg-arm-cli.md)
#### [模板](virtual-networks-create-nsg-arm-template.md)
#### [PowerShell（经典）](virtual-networks-create-nsg-classic-ps.md)
#### [CLI（经典）](virtual-networks-create-nsg-classic-cli.md)

### 用户定义路由
#### [PowerShell](virtual-network-create-udr-arm-ps.md)
#### [CLI](virtual-network-create-udr-arm-cli.md)
#### [模板](virtual-network-create-udr-arm-template.md)
#### [PowerShell（经典）](virtual-network-create-udr-classic-ps.md)
#### [CLI（经典）](virtual-network-create-udr-classic-cli.md)

### 虚拟网络对等互连
#### [门户](virtual-networks-create-vnetpeering-arm-portal.md)
#### [PowerShell](virtual-networks-create-vnetpeering-arm-ps.md)
#### [模板](virtual-networks-create-vnetpeering-arm-template-click.md)

### 虚拟机

#### 静态公共 IP 地址
##### [门户](virtual-network-deploy-static-pip-arm-portal.md)
##### [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
##### [CLI](virtual-network-deploy-static-pip-arm-cli.md)
##### [模板](virtual-network-deploy-static-pip-arm-template.md)
##### [PowerShell（经典）](virtual-networks-reserved-public-ip.md)

#### 静态专用 IP 地址
##### [门户](virtual-networks-static-private-ip-arm-pportal.md)
##### [PowerShell](virtual-networks-static-private-ip-arm-ps.md)
##### [CLI](virtual-networks-static-private-ip-arm-cli.md)
##### [门户（经典）](virtual-networks-static-private-ip-classic-pportal.md)
##### [PowerShell（经典）](virtual-networks-static-private-ip-classic-ps.md)
##### [CLI（经典）](virtual-networks-static-private-ip-classic-cli.md)

#### 多个网络接口
##### [PowerShell](virtual-network-deploy-multinic-arm-ps.md)
##### [CLI](virtual-network-deploy-multinic-arm-cli.md)
##### [模板](virtual-network-deploy-multinic-arm-template.md)
##### [PowerShell（经典）](virtual-network-deploy-multinic-classic-ps.md)
##### [CLI（经典）](virtual-network-deploy-multinic-classic-cli.md)

#### 多个 IP 地址
##### [Azure 门户](virtual-network-multiple-ip-addresses-portal.md)
##### [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)
##### [CLI](virtual-network-multiple-ip-addresses-cli.md)
##### [模板](virtual-network-multiple-ip-addresses-template.md)

### 连接方案
#### [虚拟网络 (VNet) 到 VNet](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fmooncaketest%2farticles%2fvirtual-network%2ftoc.json)
#### [VNet (Resource Manager) 到 VNet（经典）](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md?toc=%2fmooncaketest%2farticles%2fvirtual-network%2ftoc.json)
#### [VNet 到本地网络 (VPN)](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fmooncaketest%2farticles%2fvirtual-network%2ftoc.json)
#### [VNet 到本地网络 (ExpressRoute)](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fmooncaketest%2farticles%2fvirtual-network%2ftoc.json)
#### [高可用性混合网络体系结构](../guidance/guidance-hybrid-network-expressroute-vpn-failover.md?toc=%2fmooncaketest%2farticles%2fvirtual-network%2ftoc.json)

### 安全方案
#### [使用虚拟设备保护网络](virtual-network-scenario-udr-gw-nva.md)
#### [Azure 与 Internet 之间的外围网络](../guidance/guidance-iaas-ra-secure-vnet-dmz.md?toc=%2fmooncaketest%2farticles%2fvirtual-network%2ftoc.json)
#### [云服务和网络安全](../best-practices-network-security.md?toc=%2fmooncaketest%2farticles%2fvirtual-network%2ftoc.json)
##### [使用 NSG 的简单外围网络](virtual-networks-dmz-nsg-asm.md)
##### [使用防火墙和 NSG 的外围网络](virtual-networks-dmz-nsg-fw-asm.md)
##### [使用防火墙、UDR 和 NSG 的外围网络](virtual-networks-dmz-nsg-fw-udr-asm.md)
##### [示例应用程序](virtual-networks-sample-app.md)

## 配置
### 加速网络
#### [Azure 门户](virtual-network-accelerated-networking-portal.md)
#### [PowerShell](virtual-network-accelerated-networking-powershell.md)
### 访问控制列表
#### [经典门户](virtual-networks-acl.md)
#### [PowerShell](virtual-networks-acl-powershell.md)

## 管理
### 网络安全组
#### [门户](virtual-network-manage-nsg-arm-portal.md)
#### [PowerShell](virtual-network-manage-nsg-arm-ps.md)
#### [CLI](virtual-network-manage-nsg-arm-cli.md)
#### [日志](virtual-network-nsg-manage-log.md)
#### 故障排除
##### [门户](virtual-network-nsg-troubleshoot-portal.md)
##### [PowerShell](virtual-network-nsg-troubleshoot-powershell.md)
### 路由故障排除
#### [门户](virtual-network-routes-troubleshoot-portal.md)
#### [PowerShell](virtual-network-routes-troubleshoot-powershell.md)
### 虚拟机
#### [查看和修改主机名](virtual-networks-viewing-and-modifying-hostnames.md)
#### [将 VM 移到其他子网](virtual-networks-move-vm-role-to-subnet.md)

# 引用
## [PowerShell (Resource manager)](https://msdn.microsoft.com/library/mt163510(v=azure.300))
## [PowerShell（经典）](https://msdn.microsoft.com/library/mt270335(v=azure.300))
## [Azure CLI](/cli/azure/)
## [Java](/java/api/)
## [REST (Resource Manager)](https://msdn.microsoft.com/library/mt163658.aspx)
## [REST（经典）](https://msdn.microsoft.com/library/jj157182.aspx)


# 相关内容
## [虚拟机](/azure/virtual-machines/)
## [应用程序网关](/azure/application-gateway/)
## [Azure DNS](/azure/dns/)
## [流量管理器](/azure/traffic-manager/)
## [负载均衡器](/azure/load-balancer/)
## [VPN 网关](/azure/vpn-gateway/)
## [ExpressRoute](/azure/expressroute/)

# 资源
## [网络博客](http://azure.microsoft.com/blog/topics/networking)
## [网络论坛](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesVirtualNetwork)
## [价格](https://azure.microsoft.com/pricing/details/virtual-network)
## [堆栈溢出](http://stackoverflow.com/questions/tagged/azure-virtual-network)

<!---HONumber=Mooncake_0206_2017-->