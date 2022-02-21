---
title: "安装监控Agent"
date: 2019-07-19T20:59:00+08:00
weight: 10
description: >
  介绍如何为虚拟机或裸金属安装监控Agent。
---

虚拟机监控Agent采集的监控数据需要上报到平台的InfluxDB数据库中，因此需要判断虚拟机是否可以直接连接到InfluxDB数据库。

- 若虚拟机可以直接连接InfluxDB数据库，则直接[安装监控Agent](#安装监控agent)。
- 若虚拟机无法直接连接到InfluxDB数据库，请按照下面步骤安装Agent。
    - 配置SSH代理节点：建立虚拟机与InfluxDB数据库的连接；
    - 配置Remote规则：配置监控指标上报到InfluxDB数据库的数据通道。
    - 安装监控Agent：采集监控信息

### 配置SSH代理节点

#### 前提条件

请根据下面情况判断虚拟机所在VPC是否需要配置SSH代理。

- {{<oem_name>}} 平台虚拟机和裸金属默认可以直连平台InfluxDB数据库，忽略该步骤，直接跳到安装监控Agent步骤；

- 非{{<oem_name>}} 平台的VPC内的所有虚拟机若可以直接连接到平台InfluxDB数据库，可通过下面命令将虚拟机所在VPC设置为可直连VPC，忽略配置SSH代理节点步骤，直接跳到安装监控Agent步骤；

```
# 将VPC设置为可直连VPC
climc vpc-update --direct <vpc_id> 
```
- 非{{<oem_name>}} 平台的虚拟机若无法直接连接到平台InfluxDB数据库，可通过配置SSH代理步骤，使虚拟机可以连接到平台InfluxDB数据库。

#### 虚拟机配置要求

- 目前只支持Linux操作系统的虚拟机作为SSH代理节点。
- 请确保虚拟机处于运行中状态；
- 请确保虚拟机支持通过平台免密登录；虚拟机能被平台免密登录，则要求虚拟机与平台网络通（即通过EIP、NAT网关或SSH代理等方式使虚拟机与平台网络通）以及虚拟机中存在平台的公钥文件。
- 请检查虚拟机的sshd配置，GatewayPorts是clientspecified，若该项值为no，则只允许绑定127.0.0.1的地址，使remote forward无法正常使用，造成安装监控Agent的虚拟机无法向平台上报监控数据等。

#### 操作步骤

1. 在左侧导航栏，选择 **_"网络/SSH代理/SSH代理节点"_** 菜单项，进入SSH代理页面。
2. 单击列表上方 **_"新建"_** 按钮，进入新建SSH代理节点页面。
3. 在选择虚拟机页面设置以下参数：
    - 域：设置SSH代理节点所属域，并通过域过滤可选的虚拟机。
    - 名称：设置SSH代理节点的名称。
    - 区域：通过平台、区域过滤VPC。
    - 网络：通过VPC、网络过滤虚拟机。
    - 虚拟机：通过上面的筛选条件过滤出符合条件的虚拟机，并支持在搜索框中通过名称和IP搜索虚拟机，请确保所选的虚拟机符合[虚拟机配置要求](#虚拟机配置要求)，如没有合适的虚拟机，可以单击“新建”超链接，跳转到虚拟机列表页面创建符合需求的虚拟机。
4. 选择好虚拟机后，单击 **_"下一步"_** 按钮，开始探测虚拟机的免密登录状态。
    - 如虚拟机可免密登录，可直接单击 **_"确定"_** 按钮，开始创建虚拟机。
    - 如虚拟机不可免密登录，请先点击列表操作列 **_"查看"_** 按钮，查看探测免密登录失败的具体原因。
        - 如报错原因中提示“none publickey”，可通过设置免密登录功能，将虚拟机设置为免密登录状态。设置免密登录方式配置参数如下：
            - 设置方式：支持密钥、密码、脚本等方式将平台的公钥上传到虚拟机上。
            - 当设置方式为“密钥”时，请使用root用户或具有使用sudo免密权限的用户以其私钥，请确保可以通过用户名和私钥通过ssh连接到对应虚拟机，单击 **_"确定"_** 按钮，开始设置并探测虚拟机的免密登录状态是否变为免密登录。
            - 当设置方式为“密码”时，请使用root用户或具有使用sudo免密权限的用户以其密码，请确保可以通过用户名和密码通过ssh连接到对应虚拟机。单击 **_"确定"_** 按钮，开始设置并探测虚拟机的免密登录状态是否变为免密登录。
            - 当设置方式为“脚本”时，请请使用root或具有sudo权限的用户在虚拟机中执行以下脚本，执行完成后，单击 **_"确定"_** 按钮，开始设置并探测虚拟机的免密登录状态是否变为免密登录。
        - 如报错原因中提示“network error”，则需要返回上一步选择其他虚拟机，或为该虚拟机通过绑定EIP或NAT网关等方式，使其与平台网络可通。
5. 只有当虚拟机免密登录状态为“可免密登录”时，才支持单击 **_"确定"_** 按钮，开始创建SSH代理节点。
6. 在创建SSH代理节点时将会检查虚拟机的sshd配置是否符合虚拟机配置要求，若不符合将会尝试变更虚拟机的sshd配置，因此可能会造成创建ssh代理节点时间过长，若提示超时，请重新单击 **_"确定"_** 按钮，创建SSH代理节点。


### 配置Remote规则

若需要配置SSH代理在ssh代理节点上配置到InfluxDB的remote规则，使监控数据可以上报到平台的InfluxDB数据库。

```
$ climc proxy-forward-create --proxy-endpoint-id <ssh代理节点的ID> --type remote --remote-addr <influxdb的IP地址> --remote-port <InfluxDB的端口号> --bind-port-req <映射绑定的端口号> <remote规则的名称>
```
下面举例介绍如何创建对应的remote规则，即将10.127.100.2:30086地址映射为10.0.9.254:30086，后续telegraf配置中的InfluxDB地址“https://10.0.9.254:30086”

```
$ climc proxy-forward-create --proxy-endpoint-id dba57f12-4f9f-4d60-8789-7dc0fe4efc6a --type remote --remote-addr 10.127.100.2 --remote-port 30086 --bind-port-req 30086 remote-influxdb
+-------------------+--------------------------------------+
|       Field       |                Value                 |
+-------------------+--------------------------------------+
| bind_addr         | 10.0.9.254                           |
| bind_port         | 30086                                |
| bind_port_req     | 0                                    |
| can_delete        | true                                 |
| can_update        | true                                 |
| created_at        | 2021-12-09T06:30:32.000000Z          |
| deleted           | false                                |
| domain_id         | default                              |
| freezed           | false                                |
| id                | 3268655c-b816-4e4c-8250-88c67773ecff |
| is_emulated       | false                                |
| is_system         | false                                |
| last_seen_timeout | 117                                  |
| name              | remote-influxdb                      |
| pending_deleted   | false                                |
| project_src       | local                                |
| proxy_agent       | proxyagent0                          |
| proxy_agent_id    | 330e097e-59e4-4c65-8414-05d6d945e1c0 |
| proxy_endpoint    | helanzhu                             |
| proxy_endpoint_id | dba57f12-4f9f-4d60-8789-7dc0fe4efc6a |
| remote_addr       | 10.127.100.2                         |
| remote_port       | 30086                                |
| status            | init                                 |
| tenant_id         | 55bb511b62bf47dc86e82c731005ba10     |
| type              | remote                               |
| update_version    | 0                                    |
| updated_at        | 2021-12-09T06:30:32.000000Z          |
+-------------------+--------------------------------------+
```

### 安装监控Agent

#### 前提条件

安装监控Agent需要满足以下条件：

- 虚拟机或裸金属可以直接连接到平台的InfluxDB数据库；
- 虚拟机或裸金属可以被平台免密登录。
    - 属于{{<oem_name>}}平台上虚拟机或裸金属可以直接被平台免密登录。
    - 在{{<oem_name>}}平台上新建的属于其他平台的虚拟机默认也可以直接被平台免密登录。
    - 其他平台同步到{{<oem_name>}}平台上的虚拟机默认不支持被平台免密登录，需要为虚拟机[设置免密登录](#设置免密登录)

#### 设置免密登录

该功能用于用于配置相关参数使虚拟机能够免密登录，设置免密登录之前需要确保虚拟机与平台网络通。

**设置免密登录**

1. 在左侧导航栏，选择 **_"主机/主机/虚拟机"_** 菜单项，进入虚拟机页面。
2. 单击虚拟机右侧操作列 **_"更多"_** 按钮，选择 **_"密码密钥-设置免密登录"_** 菜单项，弹出设置免密登录对话框。
2. 配置以下参数：
    - 设置方式：支持密钥、密码、脚本等方式将平台的公钥上传到虚拟机上。
        - 当设置方式为“密钥”时，请使用root用户或具有使用sudo免密权限的用户以其私钥，请确保可以通过用户名和私钥通过ssh连接到对应虚拟机，单击 **_"确定"_** 按钮，进入等待执行结果页面，开始设置并探测虚拟机的免密登录状态是否变为免密登录。
        - 当设置方式为“密码”时，请使用root用户或具有使用sudo免密权限的用户以其密码，请确保可以通过用户名和密码通过ssh连接到对应虚拟机。单击 **_"确定"_** 按钮，进入等待执行结果页面，开始设置并探测虚拟机的免密登录状态是否变为免密登录。
        - 当设置方式为“脚本”时，请请使用root或具有sudo权限的用户在虚拟机中执行以下脚本，执行完成后，单击 **_"确定"_** 按钮，进入等待执行结果页面，开始设置并探测虚拟机的免密登录状态是否变为免密登录。
    - SSH端口：当虚拟机SSH默认端口22被禁用后，可通过修改SSH端口连接到虚拟机。
3. 若虚拟机可以免密登录，直接单击 **_"关闭"_** 按钮。
4. 若虚拟机仍不可免密登录，请在操作列表查看不可免密登录的原因。
    - 如报错原因中提示“Failed to connect to the host via ssh”，则需要先将该虚拟机通过绑定EIP或NAT网关以及SSH代理等方式，使其与平台网络可通。
    - 如报错原因中提示“Permission denied”，则表示输入的信息错误，可单击 **_"上一步"_** 按钮，修改配置，继续设置并探测。

#### 安装Agent

当确保虚拟机、裸金属可以连接到平台的InfluxDB数据库，且可以被平台免密登录时，可以开始安装Agent。

1. 在左侧导航栏，选择 **_"主机/主机/虚拟机"_** 菜单项，进入虚拟机页面。或者在左侧导航栏，选择 **_"主机/主机/裸金属"_** 菜单项，进入裸金属页面。
2. 单击资源名称项，进入虚拟机/裸金属详情页面。
3. 单击“监控”页签，进入监控页面。
4. 单击 **_"安装Agent"_** 按钮，直接安装Agent。


