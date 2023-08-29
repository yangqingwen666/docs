---
title: "多节点安装(已废弃)"
linkTitle: "多节点安装(已废弃)"
edition: ce
weight: 4
description: >
  使用 ocboot 部署工具在多个节点部署 Cloudpods 服务
---

{{% alert title="注意" color="warning" %}}
多节点安装的内容已经废弃，不提倡使用这种方式，推荐用户先参考 [All in One 融合云安装](../../quickstart/allinone-converge) 或者 [高可用安装](../ha) 把集群搭建好，然后再使用 [添加计算节点](../host) 的方式添加计算节点到集群。

以下内容只是作为保留作为参考。
{{% /alert %}}

多节点安装和 [All in One 融合云安装](../../quickstart/allinone-converge) 一样，都使用 https://github.com/yunionio/ocboot 这个部署工具，根据配置执行 ansible playbook 部署节点。

## 环境准备

关于环境的准备和不同架构 CPU 操作系统的要求，请参考 [All in One 融合云安装/机器配置要求](../../quickstart/allinone-converge#机器配置要求)。

以下为待部署机器的环境，假设已经准备好了 5 台机器，IP 分别是 10.127.10.156-160 ，各个节点做出以下角色规划：

- mariadb_node: 这个角色表示该节点上部署并运行 mariadb 数据库服务，该角色不一定要写在配置中，如果环境中有准备好的数据库，也可以不部署
    - 节点: 10.127.10.156
- primary_master_node: 这个角色表示该节点是第一个部署并运行 k8s master 组件的节点，该角色必须存在于配置中，该角色运行 onecloud 控制服务
    - 节点: 10.127.10.156
- master_nodes: 这个角色表示这些节点运行控制服务，该角色可选，主要作用是和 primary_master_node 一起组成 Kubernetes 的 etcd 3 节点高可用
    - 节点: 10.127.10.157-158
- worker_nodes: 这个角色表示这些节点运行私有云计算服务，该角色可选，如果不需要内置的私有云功能，可以不配置
    - 节点: 10.127.10.159-160

|         IP        | 登录用户 | 角色                               |
|:-----------------:|:--------:|------------------------------------|
|   10.127.10.156   |   root   | mariadb_node & primary_master_node |
| 10.127.10.157-158 |   root   | master_nodes                       |
| 10.127.10.159-160 |   root   | worker_nodes                       |

## 开始安装

### 下载 ocboot

参考 [All in One 融合云安装/下载 ocboot](../../quickstart/allinone-converge/#下载-ocboot)。

### 编写部署配置

```bash
# 编写 config-nodes.yml 文件
$ cat <<EOF >./config-nodes.yml
mariadb_node:
  hostname: 10.127.10.156
  user: root
  db_user: root
  db_password: your-sql-password
primary_master_node:
  onecloud_version: {{<release_version>}}
  hostname: 10.127.10.156
  user: root
  db_host: 10.127.10.156
  db_user: root
  db_password: your-sql-password
  controlplane_host: 10.127.10.156
  controlplane_port: "6443"
master_nodes:
  hosts:
  - hostname: 10.127.10.157
    user: root
  - hostname: 10.127.10.158
    user: root
  controlplane_host: 10.127.10.156
  controlplane_port: "6443"
worker_nodes:
  hosts:
  - hostname: 10.127.10.159
    user: root
  - hostname: 10.127.10.160
    user: root
  controlplane_host: 10.127.10.156
  controlplane_port: "6443"
EOF
```

### 开始部署

当填写完 config-nodes.yml 部署配置文件后，便可以执行 ocboot 里面的 `./run.py ./config-nodes.yml` 部署集群了。

```bash
# 开始部署
$ ./run.py ./config-nodes.yml
```

等待部署完成后，就可以使用浏览器访问 https://10.168.26.216 (primary_master_node 的 IP), 输入用户名 `admin` 和密码 `admin@123`，进入前端。

然后就可以[创建私有云虚拟机](../../quickstart/allinone-converge/#创建第一台虚拟机)或者[纳管公有云资源](../../quickstart/allinone-converge/#导入公有云或者其它私有云平台资源)。
