---
title: "云账号"
weight: 1
description: >
    云账号用于与私有云和公有云平台建立连接，同步相关资源并进行管理。
---

云管平台通过云账号与不同平台建立连接，并同步平台上的资源到云管平台上管理。一个账户对应的云资源归属域，不同域内资源隔离，可通过共享功能让其他域使用云账号资源。当系统未启用三级权限时，所有云资源都默认属于default域。

目前{{<oem_name>}}平台支持纳管的平台如下：

- 公有云：阿里云（公共云和金融云）、Azure、腾讯云、AWS、华为云、UCloud、谷歌云、天翼云等，后续还将陆续支持更多云平台以满足用户的需求。
- 私有云：VMware、ZStack、DStack、OpenStack、阿里飞天私有云、HCSO等；

公有云平台账单采集规则：

- 仅阿里云、AWS、Azure、华为云、Google支持配置账单文件访问信息采集账单，腾讯云可通过API采集账单信息。
- 用户配置或修改账单文件信息时，将会采集当月账单，例如：3号配置了账单文件访问信息，将会采集1~2号的账单文件；30号配置账单文件访问信息，将会采集1~29号的账单文件。1号配置账单文件访问信息，将会采集上月1~31号的账单。
- 当账单触发多次采集时，以最后一次采集结果为准。

**入口**：在云管平台单击左上角![](../../../images/intro/nav.png)导航菜单，在弹出的左侧菜单栏中单击 **_"多云管理/云账号/云账号"_** 菜单项，进入云账号页面。

![](../../../images/multiplecloud/account1.png)

## 新建云账号

{{% alert title="说明" %}}
- 如需在{{<oem_name>}}平台上管理公有云平台，至少要求云账号拥有所操作资源的管理权限。建议授予云账号平台所有功能的管理权限。
- 已添加的云账号不支持更改域，如用户需要将云账号上的资源同步到其他域，可以在{{<oem_name>}}上删除云账号，再重新添加云账号到指定域。在{{<oem_name>}}平台上删除云账号操作仅为取消纳管云账号资源，不会影响云账号上的资源。
{{% /alert %}}

### 新建阿里云账号

1. 在云账号页面单击列表上方 **_"新建"_** 按钮，进入新建云账号页面。
2. 选择云平台为阿里云，单击 **_"下一步：配置云账号"_** 按钮，进入配置云账号页面。
3. 配置以下参数：
   - 名称：阿里云账号的名称。
   - 账号类型：目前支持对接公共云和金融云的阿里云账号。
   - 密钥ID/密码：通过Access Key验证方式对接阿里云平台，Access Key由密钥ID（Access Key ID）和密码（Access Key Secret）组成。具体请参考[阿里云相关参数获取方式](#阿里云相关参数获取方式)。
   - 域：选择云账号所属的域。当云账号私有状态下，域下所有项目用户都可以使用云账号创建资源。
   - 资源归属项目：选择将云账号上的资源同步到{{<oem_name>}}平台的本地项目。如需将云账号上的资源按照云上项目归类，请先指定默认资源归属项目，并勾选自动创建项目。勾选后，将会在{{<oem_name>}}平台创建与云上项目同名的本地项目，并将资源同步到对应项目中。云上没有项目归属的资源将会同步到默认资源归属项目。
   - 代理：当云账号需要代理才可以正常访问时设置该项，留空代表直连。如没有合适的代理，直接单击“新建”超链接，在弹出的新建代理对话框中设置相关参数，创建代理。
   - 开启免密登录：启用该项后，会自动将系统的SAML信息同步到云账号上，并成为云上登录的身份提供商。实现通过本系统单点登录到公有云平台。
   - 自动同步：设置是否自动同步阿里云平台上的信息，并设置自动同步的时间。
   - 共享范围：设置云账号的共享范围，默认为不共享，则仅云账号所在域可以使用该账号，若设置为全局共享，则平台上所有用户都可以使用该云账号创建资源。
4. 单击 **_"连接测试"_** 按钮，测试输入的参数是否正确。
5. 测试成功后，单击 **_"下一步：配置同步资源区域"_** 按钮，进入配置同步资源区域页面，该配置可在云账号详情页-订阅-区域进行修改（默认同步所有区域）。如在{{<oem_name>}}平台默认同步所有区域，可直接单击 **_"跳过"_** 按钮。
6. 配置成功后，单击  **_"下一步：账单文件访问信息（可选）"_** 按钮，进入账单文件访问信息页面配置云账号的账单参数以便用户可以在费用中查看云账号的账单信息。账单文件访问信息页面选填，如不需要在{{<oem_name>}}平台查看云账号账单信息，可直接单击 **_跳过_** 按钮。如需要在{{<oem_name>}}平台中查看账单信息等，请配置相关参数，配置完成且测试成功后，单击 **_"确定"_** 按钮，并进入定时同步任务设置页面配置云账号的同步任务使得云账号自动同步行为更加可控。
{{% alert title="注意" color="warning" %}}
如果添加的阿里云账号是新账号，请先在阿里云平台上开通OSS服务。
{{% /alert %}}
   - 云账号类型：包括主账号和关联账号，使用关联账号之前请确保主账号已导入{{<oem_name>}}平台，并在使用关联账号时选择该主账号。
   - 存储桶URL：账单文件所在存储桶的URL。具体请参考[如何获取账单存储桶URL？](#如何获取账单存储桶url)。
   - 文件前缀：当账单bucket中除账单文件外还存放了其他文件时，需要配置文件前缀仅获取bucket中的账单文件等。阿里云的账单文件前缀为账号ID，可在账号管理-安全设置中查看账号ID。  
   - 账单分析范围：设置平台分析云账号账单的范围。目前仅支持本平台纳管账号。
       - 本平台纳管账号：即采集主账号及主账号关联的子账号的账单信息。如该主账号仅作为其他账号的付款账号时，采集到的其他账号的账单文件将会被丢弃。
   - 立即采集账单：{{<oem_name>}}平台默认每天凌晨4点自动采集账单。开启该项后，配置完账单文件访问信息后，将会立即采集账单。
   - 时间范围：当启用立即采集账单后，支持设置时间范围，立即采集时间范围内的账单，请确保在选择的时间范围内有账单数据。建议采集1~6个月内的账单，否则会因为数据太多，造成系统压力多大影响日常采集账单的任务。
7. 定时同步任务设置页面选填，如不需要在{{<oem_name>}}平台设置自动同步任务，可直接单击 **_"跳过"_** 按钮。如需要在{{<oem_name>}}平台中设置云账号自动同步的时间，请配置相关参数，配置完成且测试通过后，单击 **_"确定"_** 按钮，创建阿里云账号。
 

#### 阿里云相关参数获取方式

##### 主账号获取AccessKey

1. 使用主账号登录阿里云控制台，单击页面右上角个人信息，展开下拉菜单，单击 **_"accesskeys** "_** 菜单项进入安全信息管理页面。
   ![](../../../../faq/image/aliyun-accesskeys.png)

2. 在安全信息管理页面，可以查看已存在的AccessKey信息，也可以单击 **_"创建AccessKey"_** 按钮新建用户AccessKey，新建AccessKey时阿里云会向账号联系人手机发送验证码，验证通过后才可以创建AccessKey。
   ![](../../../../faq/image/aliyun-get_acceesskey_list.png)

3. Access Key Secret默认不显示，单击"**显示** "链接，阿里云将向账号所属的联系人手机发送一个验证码，验证通过后，才会显示Access Key Secret。
   ![](../../../../faq/image/aliyun-get_access_key_secret.png)

##### RAM子账号如何获取Access Key

1. 使用子账号登录阿里云控制台，单击页面右上角个人信息，展开下拉菜单，单击 "**accesskey...**" 进入安全信息管理页面。
   ![](../../../../faq/image/aliyun_ram_get_access_key.png)

2. 在安全信息管理页面，单击 **_"创建AccessKey"_** 按钮，创建AccessKey。
   ![](../../../../faq/image/aliyun_get_ram_access_key_create.png)

3. 创建成功后，AccessKeySecret信息只会展示一次，请及时保存。
   ![](../../../../faq/image/aliyun_ram_access_key_get.png)

{{% alert title="注意" color="warning" %}}
已创建的AccessKey，无法再查看AccessKeySecret。
{{% /alert %}}
 
##### 通过平台管理阿里云资源，需要云账号拥有哪些权限

使用{{<oem_name>}}管理阿里云资源，需要接入云账号的有足够的权限，下面列出管理云资源所用到的权限策略，如果由于接入账号未被授权导致的错误提示，请按照以下说明对接入账号进行授权：

| 功能                               | 只读权限                                          | 可读可写权限                                 |
| :----------                        | :--------                                         | :----------                                  |
| 所有功能总和                       | ReadOnlyAccess                                    | AdministratorAccess                          |
| 虚拟机, 安全组, 镜像, 磁盘, 快照   | AliyunECSReadOnlyAccess                           | AliyunECSFullAccess                          |
| Vpc, Vpc对等连接, 路由表           | AliyunVPCReadOnlyAccess                           | AliyunVPCFullAccess                          |
| Eip                                | AliyunEIPReadOnlyAccess                           | AliyunEIPFullAccess                          |
| 弹性网卡                           | AliyunVPCNetworkIntelligenceReadOnlyAccess        | AliyunECSNetworkInterfaceManagementAccess    |
| 对象存储                           | AliyunOSSReadOnlyAccess                           | AliyunOSSFullAccess                          |
| NAT                                | AliyunNATGatewayReadOnlyAccess                    | AliyunNATGatewayFullAccess                   |
| 负载均衡                           | AliyunSLBReadOnlyAccess<br>AliyunALBFullAccess    | AliyunSLBFullAccess<br>AliyunALBFullAccess   |
| RDS                                | AliyunRDSReadOnlyAccess                           | AliyunRDSFullAccess                          |
| 弹性缓存                           | AliyunKvstoreReadOnlyAccess                       | AliyunKvstoreFullAccess                      |
| 操作日志                           | AliyunActionTrailFullAccess                       | AliyunActionTrailFullAccess                  |
| NAS                                | AliyunNASReadOnlyAccess                           | AliyunNASFullAccess                          |
| WAF                                | AliyunYundunWAFReadOnlyAccess                     | AliyunYundunWAFFullAccess                    |
| IAM                                | AliyunRAMReadOnlyAccess                           | AliyunRAMFullAccess                          |
| DNS                                | AliyunDNSReadOnlyAccess<br>AliyunPubDNSFullAccess | AliyunDNSFullAccess<br>AliyunPubDNSFullAccess|
| 账单,余额,费用                     | AliyunFinanceConsoleReadOnlyAccess                | AliyunFinanceConsoleFullAccess               |
| 监控                               | AliyunCloudMonitorReadOnlyAccess                  | AliyunCloudMonitorFullAccess                 |

##### 如何给子账号授权

1. 使用主账号登录阿里云控制台，单击页面右上角个人信息，展开下拉菜单，单击 **_"访问控制"_** 菜单项 ，进入访问控制页面。
   ![](../../../../faq/image/aliyun_access_control.png)

2. 单击左侧菜单栏 **_"用户管理"_** 菜单项，进入用户管理页面。
   ![](../../../../faq/image/aliyun_access_control_all.png)

3. 在用户管理页面，单击指定用户操作列 **_"授权"_** 按钮，进行授权操作。使用{{<oem_name>}}管理阿里云资源的账户所必须拥有的权限请查看[通过平台管理阿里云资源，子账号需要拥有哪些权限](#通过平台管理阿里云资源-子账号需要拥有哪些权限) 。
   ![](../../../../faq/image/aliyun_ram_user_access_control.png)

##### 如何获取账单存储桶URL？
    
1. 以阿里云主账号为例，以主账号登录阿里云控制台，单击顶部[费用]菜单的下拉菜单 **_"用户中心"_** 菜单项，进入费用用户中心页面。
   ![](../../../../faq/image/aliyunusercenter.png)

2. 单击 **_"账单数据存储"_** 按钮，进入账单数据存储页面。
   ![](../../../../faq/image/aliyunusercenterhome.png)

3. 查看并记录计费项消费明细和分账账单按天汇总的bucket名称，如未设置，需要在该页面添加存储文件的订阅上述两个账单到同一bucket，设置完成后，每天的增量账单数据将同步存储到对应的OSS上。建议该bucket中仅存放账单文件。
   ![](../../../../faq/image/aliyunossbucket1.png)

{{% alert title="说明" %}}
由于阿里云OSS等类型资源的标签在计费项消费明细中账单中没有，仅在分账账单里显示，因此如需用费用上的标签分析费用，请配置分账账单按天汇总到存储桶。
{{% /alert %}}

4. 在阿里云控制台的对象存储页面中，查看对应bucket的概览信息，bucket域名即为存储桶URL。
   ![](../../../../faq/image/aliyunbucketurl.png) 


### 新建AWS账号

1. 在公有云账号页面单击列表上方 **_"新建"_** 按钮，进入新建云账号页面。
2. 选择云平台为AWS，单击 **_"下一步：配置云账号"_** 按钮，进入配置云账号页面。
3. 配置以下参数：
   - 名称：AWS账号的名称。
   - 账号类型：目前支持对接全球区和中国区的AWS云账号。
   - 密钥ID/密码：对接AWS平台的密钥ID和密码信息。具体请参考[AWS相关参数获取方式](#aws相关参数获取方式)。如需纳管AWS组织账户，请参考[如何纳管AWS Organization组织账户](#如何纳管aws-organizations组织账户)。其中AWS Organization关联的组织账号将会以云订阅的形式展示。
   - 域：选择云账号所属的域。当云账号私有状态下，域下所有项目用户都可以使用云账号创建资源。
   - 资源归属项目：选择将云账号上的资源同步到{{<oem_name>}}平台的本地项目。如需将云账号上的资源按照云上项目归类，请先指定默认资源归属项目，并勾选自动创建项目。勾选后，将会在{{<oem_name>}}平台创建与云上项目同名的本地项目，并将资源同步到对应项目中。云上没有项目归属的资源将会同步到默认资源归属项目。
   - 代理：当云账号需要代理才可以正常访问时设置该项，留空代表直连。如没有合适的代理，直接单击“新建”超链接，在弹出的新建代理对话框中设置相关参数，创建代理。
   - 开启免密登录：启用该项后，会自动将系统的SAML信息同步到云账号上，并成为云上登录的身份提供商。实现通过本系统单点登录到公有云平台。
   - 自动同步：设置是否自动同步AWS平台上的信息，并设置自动同步的时间间隔。
4. 单击 **_"连接测试"_** 按钮，测试输入的参数是否正确。
5. 测试成功后，单击 **_"下一步：配置同步资源区域"_** 按钮，进入配置同步资源区域页面，该配置可在云账号详情页-订阅-区域进行修改（默认同步所有区域）。如在{{<oem_name>}}平台默认同步所有区域，可直接单击 **_"跳过"_** 按钮。
6. 配置成功后，单击  **_"下一步：账单文件访问信息（可选）"_** 按钮，进入账单文件访问信息页面配置云账号的账单参数以便用户可以在费用中查看云账号的账单信息。账单文件访问信息页面选填，如不需要在{{<oem_name>}}平台查看云账号账单信息，可直接单击 **_跳过_** 按钮。如需要在{{<oem_name>}}平台中查看账单信息等，请配置相关参数，配置完成且测试成功后，单击 **_"确定"_** 按钮，并进入定时同步任务设置页面配置云账号的同步任务使得云账号自动同步行为更加可控。
   - 云账号类型：包括主账号和关联账号，使用关联账号之前请确保主账号已导入{{<oem_name>}}平台，并在使用关联账号时选择该主账号。
   - 存储桶URL：账单文件所在存储桶的URL。具体请参考[如何获取存储桶URL？](#如何获取账单存储桶url-1)。
   - 文件前缀：当账单bucket中除账单文件外还存放了其他文件时，需要配置文件前缀仅获取bucket中的账单文件等。AWS的文件前缀为账号ID。 
   - 账单分析范围：设置平台分析云账号账单的范围。包括本平台纳管账号和所有账号。
       - 本平台纳管账号：即采集主账号及主账号关联的组织账号的账单信息。如该AWS账号仅作为其他AWS的付款账号时，采集到的其他AWS账号的账单文件将会被丢弃。
       - 所有账单：将会采集主账号的所有账单，其中无法在平台找到对应云账号的账单条目，其云订阅将会显示为“本云账号名称-该账单条目关联云账号的数字ID”。
   - 立即采集账单：{{<oem_name>}}平台默认每天凌晨4点自动采集账单。开启该项后，配置完账单文件访问信息后，将会立即采集账单。
   - 时间范围：当启用立即采集账单后，支持设置时间范围，立即采集时间范围内的账单，请确保在选择的时间范围内有账单数据。建议采集1~6个月内的账单，否则会因为数据太多，造成系统压力多大影响日常采集账单的任务。
7. 定时同步任务设置页面选填，如不需要在{{<oem_name>}}平台设置自动同步任务，可直接单击 **_"跳过"_** 按钮。如需要在{{<oem_name>}}平台中设置云账号自动同步的时间，请配置相关参数，配置完成且测试通过后，单击 **_"确定"_** 按钮，创建AWS账号。
  

#### AWS相关参数获取方式

##### 获取AWS的访问密钥

1. 使用AWS主账号（或拥有Administrator Access管理权限的子账号）登录AWS管理控制台，单击 **_"IAM"_** 菜单项，进入IAM控制面板页面。
   ![](../../../../faq/image/faq_account_aws_1.png) 

2. 单击左侧菜单栏 **_"用户"_** 菜单项，进入用户管理列表，单击用户名名称项，进入指定用户详情页面。注意需要选择有足够管理权限的用户。
   ![](../../../../faq/image/faq_account_aws_2.png)

3. 单击“**安全证书**”页签。
   ![](../../../../faq/image/faq_account_aws_3.png)

4. 单击 **_"创建访问密钥"_** 按钮，在弹出的创建访问密钥对话框中即可看到密钥信息，即密钥ID（Access Key ID）、密码（Access Key Secret）。
   ![](../../../../faq/image/faq_account_aws_4.png)

{{% alert title="注意" color="warning" %}}
私有访问密钥仅创建时可见，请复制另存，如果不慎丢失，重新创建即可。
{{% /alert %}}

##### 通过平台管理AWS资源，需要云账号具备哪些权限？

| 功能                                              | 只读权限                                          | 可读可写权限                                 |
| :----------                                       | :--------                                         | :----------                                  |
| 所有功能总和                                      | ReadOnlyAccess                                    | AdministratorAccess                          |
| 虚拟机, 磁盘, 安全组, 镜像, 快照, 磁盘, 镜像      | AmazonEC2ReadOnlyAccess                           | AmazonEC2FullAccess                          |
| 项目                                              | -                                                 | -                                            |
| Vpc, Vpc对等连接, 路由表, NAT, 弹性网卡,EIP, NAT  | AmazonVPCReadOnlyAccess                           | AmazonVPCFullAccess                          |
| 对象存储                                          | AmazonS3ReadOnlyAccess                            | AmazonS3FullAccess                           |
| 负载均衡                                          | ElasticLoadBalancingReadOnly                      | ElasticLoadBalancingFullAccess               |
| RDS                                               | AmazonRDSReadOnlyAccess                           | AmazonRDSFullAccess                          |
| 弹性缓存                                          | AmazonElastiCacheReadOnlyAccess                   | AmazonElastiCacheFullAccess                  |
| 操作日志                                          | AWSCloudTrailReadOnlyAccess                       | AWSCloudTrail_FullAccess                     |
| NAS                                               | AmazonElasticFileSystemReadOnlyAccess             | AmazonElasticFileSystemFullAccess            |
| WAF                                               | AWSWAFReadOnlyAccess                              | AWSWAFFullAccess                             |
| IAM                                               | IAMReadOnlyAccess                                 | IAMFullAccess                                |
| DNS                                               | AmazonRoute53DomainsReadOnlyAccess                | AmazonRoute53DomainsFullAccess               |
| 账单,费用                                         | AWSBillingReadOnlyAccess                          | Billing                                      |
| 监控                                              | CloudWatchReadOnlyAccess                          | CloudWatchFullAccess                         |

##### 如何获取账单存储桶URL？


**新版**

2019/08/07日期之后创建的AWS账号必须采用该方式配置并获取存储桶的URL和文件前缀。

1. 使用AWS主账号登录AWS管理控制台，单击右上角[用户名]的下拉菜单 **_"我的账单控制面板"_** 菜单项，进入账单和成本管理控制面板页面。
    
    ![](../../../../faq/image/awsbilling.png)

2. 单击左侧菜单 **_"Cost & Usage Reoports"_** 菜单项，在AWS成本和使用率报告页面，单击 **_"创建报告"_** 按钮，进入创建报告页面。

    ![](../../../../faq/image/awscostreport.png)

3. 配置报告名称、勾选“包括资源ID”，单击 **_"下一步"_** 按钮，进入交付选项页面。

    ![](../../../../faq/image/awscreatecostreport.png)

4. 配置S3存储桶，支持选择已有的存储桶或创建新的存储桶。

    ![](../../../../faq/image/awscosts3.png)
    ![](../../../../faq/image/awscosts3policy.png)

5. 配置报告路径前缀、时间粒度选择“每小时”、报告版本为“创建新报告版本”、压缩类型选择“ZIP”，单击 **_"下一步"_** 按钮，进入审核页面。

    ![](../../../../faq/image/awscostreportconfig.png)

6. 确认配置无误后，记录红框中的S3存储桶和报告路径前缀，单击 **_"查看和完成"_** 按钮，完成配置，创建报告。

    ![](../../../../faq/image/awscostreportfinish.png)

7. 在AWS控制台的S3存储管理页面中查看对应存储桶中任意账单文件的概述信息，并记录对象URL，存储桶URL即为去掉后面文件名称的URL，如红框所示。

    ![](../../../../faq/image/awscosts3bucketurl.png)

8. 文件前缀即为步骤6中红框中的报告路径前缀。

**旧版**

1. 使用AWS主账号登录AWS管理控制台，单击右上角[用户名]的下拉菜单 **_"我的账单控制面板"_** 菜单项，进入账单和成本管理控制面板页面。
    
    ![](../../../../faq/image/awsbilling.png)

2. 单击左侧菜单 **_"账单首选项"_** ，在首选项页面的“成本管理首选项”中查看并记录“接收账单报告”的S3存储桶，如未配置，需要勾选“接收账单报告”并配置S3存储桶并验证，设置完成后，将根据设置的粒度将增量账单数据将同步存储到对应的OSS上。建议该bucket中仅存放账单文件。
    
    ![](../../../../faq/image/awsbillingbucket.png)
   
3. 在AWS控制台的S3存储管理页面中查看对应存储桶中任意账单文件的概述信息，并记录对象URL，存储桶URL即为去掉后面文件名称的URL，如红框所示。
    
    ![](../../../../faq/image/awsbillingbucketurl.png)

4. AWS的文件前缀为AWS账号ID。

{{% alert title="说明" %}}
当账单bucket中除账单文件外还存放了其他文件时，需要配置文件前缀仅获取bucket中的账单文件等。
{{% /alert %}}


#### 如何纳管AWS Organizations组织账户?

1. 配置AWS Organizations：使用AWS组织账号关联AWS账户，支持创建新的AWS账户和邀请现有的AWS账户；被邀请的AWS账户上需要存在“OrganizationAccountAccessRole”角色。
2. 获取访问密钥：在AWS组织账号上的管理账号的IAM用户创建访问密钥，建议使用具有AdministratorAccess权限的用户。

##### 配置AWS Organizations

1. 使用AWS主账号（或拥有AdministratorAccess管理权限的子账号）登录AWS管理控制台，单击右上角[用户名]的下拉菜单 **_"我的账单控制面板"_** 菜单项，进入账单和成本管理控制面板页面。

    ![](../../../../faq/image/awsbilling.png)

2. 单击右侧 **_"整合账单"_** 菜单项，进入AWS Organizations页面。

    ![](../../../../faq/image/awsorgmenu.png)

3. 在AWS Organizations - AWS 账户页面，添加AWS账户，目前支持两种将AWS账号添加到Organization的方式。
    - 创建AWS账户：设置AWS账户名、账户拥有者的电子邮件地址以及IAM角色名称（OrganizationAccountAccessRole），单击 **_"创建AWS账户"_** 按钮，创建AWS账户。
        
        ![](../../../../faq/image/awscreateorgaccount.png)
    - 邀请现有AWS账户：设置要邀请的AWS账户的电子邮件地址或账户ID，单击 **_"发送邀请"_** 按钮，等待账户拥有者接收请求，加入Organizations，此外还需要现有的AWS账号存在OrganizationAccountAccessRole的角色，如不存在请参考[如何在AWS账户中添加OrganizationAccountAccessRole的角色?](#如何在aws账户中添加organizationaccountaccessrole的角色)。
        
        ![](../../../../faq/image/awsorginviteaccount.png)

##### 获取访问密钥

1. 在AWS Organizations的管理账户上获取访问密钥，建议使用具有AdministratorAccess权限的IAM用户，创建访问密钥。
2. 获取访问密钥的具体步骤，请参考[获取AWS的访问密钥](#获取aws的访问密钥)。

##### 如何在AWS账户中添加OrganizationAccountAccessRole的角色?

1. 使用AWS主账号（或拥有AdministratorAccess管理权限的子账号）登录AWS管理控制台，单击 **_"IAM"_** 菜单项，进入IAM控制面板页面。
2. 单击右侧 **_"角色"_** 菜单项，在角色页面，单击 **_"创建角色"_** 按钮，进入创建角色页面。

    ![](../../../../faq/image/awscreaterole.png)

3. 选择受信任实体的类型为“其他AWS账户”,并填入管理AWS组织的账号ID，单击 **_"下一步：权限"_** 按钮。
    
    ![](../../../../faq/image/awsroleconfig.png)

4. Attach 权限策略选择“AdministratorAccess”，单击 **_"下一步：标签"_** 按钮。
    
    ![](../../../../faq/image/awsroleconfigpolicy.png)

5. 请根据需求配置标签，配置完成后，单击 **_"下一步：审核"_** 按钮。
6. 配置角色名称为“OrganizationAccountAccessRole”，单击 **_"创建角色"_** 按钮。

    ![](../../../../faq/image/awsroleconfigconfirm.png)


### 新建Azure账号

1. 在公有云账号页面单击列表上方 **_"新建"_** 按钮，进入新建云账号页面。
2. 选择云平台为Azure，单击 **_"下一步：配置云账号"_** 按钮，进入配置云账号页面。
3. 配置以下参数：
   - 名称：Azure账号的名称
   - 账号类型：目前支持对接全球区、中国区、美国政务区、德国区的Azure云账号。
   - 租户（Tenant）ID/客户端ID/客户端密码请参考[Azure相关参数获取方式](#azure相关参数获取方式)。
   - 域：选择云账号所属的域。当云账号私有状态下，域下所有项目用户都可以使用云账号创建资源。
   - 资源归属项目：选择将云账号上的资源同步到{{<oem_name>}}平台的本地项目。如需将云账号上的资源按照云上项目归类，请先指定默认资源归属项目，并勾选自动创建项目。勾选后，将会在{{<oem_name>}}平台创建与云上项目同名的本地项目，并将资源同步到对应项目中。云上没有项目归属的资源将会同步到默认资源归属项目。
   - 代理：当云账号需要代理才可以正常访问时设置该项，留空代表直连。如没有合适的代理，直接单击“新建”超链接，在弹出的新建代理对话框中设置相关参数，创建代理。
   - 开启免密登录：启用该项后，系统成为云上登录的身份提供商。实现通过本系统单点登录到公有云平台。目前仅Azure全球区支持免密登录的功能，此外还需要在Azure平台上做一下必要配置，具体请参考[配置Azure External Identies](#配置azure-external-identies)以及[设置Chrome浏览器](#设置chrome浏览器)。
   - 自动同步：设置是否自动同步Azure平台上的信息，并设置自动同步的时间间隔。
4. 单击 **_"连接测试"_** 按钮，测试输入的参数是否正确。
5. 测试成功后，单击 **_"下一步：配置同步资源区域"_** 按钮，进入配置同步资源区域页面，该配置可在云账号详情页-订阅-区域进行修改（默认同步所有区域）。如在{{<oem_name>}}平台默认同步所有区域，可直接单击 **_"跳过"_** 按钮。
6. 配置成功后，单击  **_"下一步：账单文件访问信息（可选）"_** 按钮，进入账单文件访问信息页面配置云账号的账单参数以便用户可以在费用中查看云账号的账单信息。账单文件访问信息页面选填， 非EA账户或无需在{{<oem_name>}}平台上管理账单数据时，可单击 **_"跳过"_** 按钮。如需要在{{<oem_name>}}平台中查看账单信息等，请配置相关参数。
7. EA（Enterprise Agreement）账户支出通过合约编号和密钥获取账单信息，请配置相关参数，配置完成并测试成功后，单击 **_"确定"_** 按钮，并进入定时同步任务设置页面配置云账号的同步任务使得云账号自动同步行为更加可控。
   - 合约编号：在线高级服务协议关联的唯一标识符，V570开头的数字。
   - 密钥：API访问密钥。具体请参考[如何获取Azure合约编号和密钥](#如何获取azure合约编号和密钥)。
   - 账单分析范围：设置平台分析云账号账单的范围。包括本平台纳管账号和所有账号。
       - 本平台纳管账号：即采集主账号及主账号关联的组织账号的账单信息。如该Azure账号仅作为其他Azure的付款账号时，采集到的其他Azure账号的账单文件将会被丢弃。
       - 所有账单：将会采集主账号的所有账单，其中无法在平台找到对应云账号的账单条目，其云订阅将会显示为“本云账号名称-该账单条目关联云账号的数字ID”。
   - 立即采集账单：{{<oem_name>}}平台默认每天凌晨4点自动采集账单。开启该项后，配置完账单文件访问信息后，将会立即采集账单。
   - 时间范围：当启用立即采集账单后，支持设置时间范围，立即采集时间范围内的账单，请确保在选择的时间范围内有账单数据。建议采集1~6个月内的账单，否则会因为数据太多，造成系统压力多大影响日常采集账单的任务。
8. 定时同步任务设置页面选填，如不需要在{{<oem_name>}}平台设置自动同步任务，可直接单击 **_"跳过"_** 按钮。如需要在{{<oem_name>}}平台中设置云账号自动同步的时间，请配置相关参数，配置完成且测试通过后，单击 **_"确定"_** 按钮，创建Azure账号。


#### Azure相关参数获取方式

##### 获取Azure的租户（Tenant）ID和Client信息

1. 登录Azure控制台，单击左侧导航栏 **_"Azure Active Directory/应用注册"_** 菜单项，进入应用注册页面。建议新建一个专门的应用程序供云管平台调用Azure API。
   ![](../../../../faq/image/azureregisterapp.png)

2. 单击 **_新注册_** 按钮，在进入的注册应用程序页面，设置名称为任意值、设置受支持的账户类型为“仅此目录中的账户”，重定向URI设置为web，并输入以"[https://](https://)"或"[http://localhost](http://localhost)"开头的URL地址，单击 **_"注册"_** 按钮。
   ![](../../../../faq/image/azureregisteredapp.png)

3. 创建成功后，系统自动显示刚创建的应用程序详情页面。该页面的应用程序（客户端）ID即为所需的客户端ID、目录（租户）ID即为所需的租户ID。
   ![](../../../../faq/image/azureclientid.png)

4. 在应用程序详情页面单击 **_"证书和密码"_** 菜单项。进入证书和密码页面。单击 **_"新客户端密码"_** 按钮。
   ![](../../../../faq/image/azureclientsecretlist.png)

5. 在弹出的添加客户端对话框输入密码说明、截止日期为“从不”，单击 **_"添加"_** 按钮新建客户端密码。
   ![](../../../../faq/image/azurecreatesecret.png)

6. 保存成功后，页面密码的值即为需要的客户端密码信息。
   ![](../../../../faq/image/azureclientsecret.png)

##### 如何把订阅的权限授权给应用程序

1. 登录Azure控制台，单击左侧导航栏 **_"所有服务"_** 菜单项，在所有服务列表中选择并单击 **_"订阅"_** 菜单项，进入订阅列表。
   ![](../../../../faq/image/azuresub.png)

2. 单击需要被授权的订阅，进入订阅的详情页面；
   ![](../../../../faq/image/azuresublist.png)

3. 单击[访问控制(标识和访问管理)]，在进入的访问控制页面中单击 **_"添加角色分配"_** 按钮，进入添加角色分配页面。
   ![](../../../../faq/image/azuresubrole.png)

4. 角色为“所有者”，单击 **_"下一步"_** 按钮，将访问权限分配到对话框为“用户、组或服务主体”，单击 **_"选择成员"_** 按钮，在选择搜索框中搜索上一步骤创建的应用程序的名称，并选中应用程序，单击 **_"下一步"_** 按钮，再单击 **_"审阅和分配"_** 按钮。

   ![](../../../../faq/image/azure1.png)
   ![](../../../../faq/image/azure2.png)
   ![](../../../../faq/image/azure3.png)
   ![](../../../../faq/image/azure4.png)
5. 在角色分配页面，查看订阅的权限已授权给应用程序。

   ![](../../../../faq/image/azure5.png)

##### 应用程序API权限设置

请确保应用程序拥有Azure Active Directory API下的以下权限。

区域 | API权限
---------|----------
 Azure中国 | Directory: Directory.Read.All, Directory.ReadWrite.All</br> Domain: Domain.Read.All
 Azure国际区 | Directory: Directory.Read.All, Directory.ReadWrite.All</br> Domain: Domain.Read.All, Domain.ReadWrite.All; </br>Member:  Member.Read.Hidden; </br>Policy: Policy.Read.All;
 
**查看及设置步骤**

以Azure国内区为例。

1. 在Azure控制台，单击左侧导航栏 **_"Azure Active Directory/应用注册"_** 菜单项，进入应用注册页面。
2. 在新注册的应用程序详情页面，单击 **_"API权限"_** 菜单项，进入API权限页面，查看API权限。

    ![](../../../../faq/image/azureapilist.png)

3. 检查应用程序的API权限是否满足上面的要求，如不满足，单击 **_"添加权限"_** 按钮，弹出请求获取API权限对话框。

    ![](../../../../faq/image/azurerequestapi1.png)

4. 选择“Azure Active Directory”，应用程序选择“应用程序权限”，并勾选Directory和Domian下的所有权限，单击 **_"添加权限"_** 按钮，完成配置。

    ![](../../../../faq/image/azurecreateapi1.png)

##### 管理Azure云资源，需要云账号具备哪些权限

| 功能                                                      | 只读权限                                              | 可读可写权限                                                      |
| :----------                                               | :--------                                             | :----------                                                       |
| 所有功能总和                                              | Reader                                                | Owner                                                             |
| 虚拟机, 磁盘, 安全组, 镜像, 快照, 磁盘, 镜像, 负载均衡    | -                                                     | Virtual Machine Contributor<br>Classic Virtual Machine Contributor|
| 项目                                                      | -                                                     | -                                                                 |
| Vpc, Vpc对等连接, 路由表, NAT, 弹性网卡,EIP, NAT, WAF     | -                                                     | Network Contributor,<br>Classic Network Contributor               |
| 对象存储                                                  | Storage Blob Data Reader                              | Storage Blob Data Owner                                           |
| RDS                                                       | Cloud SQL Viewer                                      | Cloud SQL Admin                                                   |
| 弹性缓存                                                  | Redis Enterprise Cloud Viewer                         | Redis Enterprise Cloud Admin                                      |
| NAS                                                       | Storage File Data SMB Share Reader                    | Storage File Data SMB Share Contributor                           |
| WAF                                                       | -                                                     | -                                                                 |
| IAM                                                       | -                                                     | Graph Owner<br>Resource Policy Contributor                        |
| DNS                                                       | -                                                     | DNS Zone Contributor<br>Private DNS Zone Contributor              |
| 账单,费用                                                 | Billing Reader<br>Cost Management Reader              | Cost Management Contributor                                       |
| 监控,操作日志                                             | Monitoring Reader                                     | Monitoring Contributor                                            |

##### 如何获取Azure合约编号和密钥

1. 登录[Azure中国EA Portal](https://ea.azure.cn/)or[Azure EA Portal](https://ea.azure.com/)，登录系统后，左上角数字即为合约编号。
   ![](../../../../faq/image/azure_number.png)

2. 单击左侧导航栏 **_"报表"_** 菜单项，选择“下载使用量>API访问密钥”页签，该页面的主密钥即为密钥。
   ![](../../../../faq/image/azure_apikey.png) 

### 新建华为云账号

1. 在云账号页面单击列表上方 **_"新建"_** 按钮，进入新建云账号页面。
2. 选择云平台为华为云，单击 **_"下一步：配置云账号"_** 按钮，进入配置云账号页面。
3. 配置以下参数：
   - 名称：华为云账号的名称。
   - 账号类型：目前支持对接中国区的华为云账号。
   - 密钥ID/密码：对接华为云平台的密钥ID和密码信息。具体请参考[华为云相关参数获取方式](#华为云相关参数获取方式)。
   - 域：选择云账号所属的域。当云账号私有状态下，域下所有项目用户都可以使用云账号创建资源。
   - 资源归属项目：选择将云账号上的资源同步到{{<oem_name>}}平台的本地项目。如需将云账号上的资源按照云上项目归类，请先指定默认资源归属项目，并勾选自动创建项目。勾选后，将会在{{<oem_name>}}平台创建与云上项目同名的本地项目，并将资源同步到对应项目中。云上没有项目归属的资源将会同步到默认资源归属项目。
   - 代理：当云账号需要代理才可以正常访问时设置该项，留空代表直连。如没有合适的代理，直接单击“新建”超链接，在弹出的新建代理对话框中设置相关参数，创建代理。
   - 开启免密登录：启用该项后，会自动将系统的SAML信息同步到云账号上，并成为云上登录的身份提供商。实现通过本系统单点登录到公有云平台。
   - 自动同步：设置是否自动同步腾讯云平台上的信息，并设置自动同步的时间间隔。
   - 共享范围：设置云账号的共享范围，默认为不共享，则仅云账号所在域可以使用该账号，若设置为全局共享，则平台上所有用户都可以使用该云账号创建资源。
4. 单击 **_"连接测试"_** 按钮，测试输入的参数是否正确。
5. 测试成功后，单击 **_"下一步：配置同步资源区域"_** 按钮，进入配置同步资源区域页面，该配置可在云账号详情页-订阅-区域进行修改（默认同步所有区域）。如在{{<oem_name>}}平台默认同步所有区域，可直接单击 **_"跳过"_** 按钮。
6. 配置成功后，单击  **_"下一步：账单文件访问信息（可选）"_** 按钮，进入账单文件访问信息页面配置云账号的账单参数以便用户可以在费用中查看云账号的账单信息。账单文件访问信息页面选填，如不需要在{{<oem_name>}}平台查看云账号账单信息，可直接单击 **_跳过_** 按钮。如需要在{{<oem_name>}}平台中查看账单信息等，请配置相关参数，配置完成且测试成功后，单击 **_"确定"_** 按钮，并进入定时同步任务设置页面配置云账号的同步任务使得云账号自动同步行为更加可控。
   - 云账号类型：包括主账号和关联账号，使用关联账号之前请确保主账号已导入{{<oem_name>}}平台，并在使用关联账号时选择该主账号。
   - 存储桶URL：账单文件所在存储桶的URL。具体请参考[如何获取账单存储桶的URL？](#如何获取账单存储桶url-2)。
   - 账单分析范围：设置平台分析云账号账单的范围。目前仅支持本平台纳管账号。
       - 本平台纳管账号：即采集主账号及主账号关联的子账号的账单信息。如该主账号仅作为其他账号的付款账号时，采集到的其他账号的账单文件将会被丢弃。
   - 立即采集账单：{{<oem_name>}}平台默认每天凌晨4点自动采集账单。开启该项后，配置完账单文件访问信息后，将会立即采集账单。
   - 时间范围：当启用立即采集账单后，支持设置时间范围，立即采集时间范围内的账单，请确保在选择的时间范围内有账单数据。建议采集1~6个月内的账单，否则会因为数据太多，造成系统压力多大影响日常采集账单的任务。
7. 定时同步任务设置页面选填，如不需要在{{<oem_name>}}平台设置自动同步任务，可直接单击 **_"跳过"_** 按钮。如需要在{{<oem_name>}}平台中设置云账号自动同步的时间，请配置相关参数，配置完成且测试通过后，单击 **_"确定"_** 按钮，创建华为云账号。

#### 华为云相关参数获取方式

##### 如何获取华为云的API密钥

**新版**

1. 登录华为云控制台，鼠标悬停在右上角用户名处，选择下拉菜单 **_"我的凭证"_** 菜单项，进入我的凭证页面。

    ![](../../../../faq/image/huaweinewaccount.png)
2. 单击左侧[访问密钥]菜单，在访问密钥页面单击 **_"新增访问密钥"_** 按钮。

    ![](../../../../faq/image/huaweinewak.png)

3. 通过验证后，会下载credentials名称的Excel表格，打开表格后即可获取密钥ID（Access Key ID）和密码（Secret Access Key）。
    ![](../../../../faq/image/faq_account_huawei_3.png)

**旧版**

1. 登录华为云控制台，鼠标悬停在右上角用户名处，选择下拉菜单 **_"我的凭证"_** 菜单项，进入我的凭证页面。
     ![](../../../../faq/image/faq_account_huawei_1.png)
2. 单击“**管理访问密钥**”页签，在管理访问密钥页面单击 **_"新增访问密钥"_** 按钮。
     ![](../../../../faq/image/faq_account_huawei_2.png)
3. 通过验证后，会下载credentials名称的Excel表格，打开表格后即可获取密钥ID（Access Key ID）和密码（Secret Access Key）。
     ![](../../../../faq/image/faq_account_huawei_3.png)

##### 通过平台管理华为云资源，需要云账号具备哪些权限

| 功能                                          | 只读权限                                          | 可读可写权限                                     |
| :----------                                   | :--------                                         | :----------                                      |
| 所有功能总和                                  | Tenant Guest<br>IAM ReadOnlyAccess                | Tenant Administrator<br>Security Administrator   |
| 虚拟机                                        | ECS ReadOnlyAccess                                | ECS FullAccess                                   |
| 磁盘, 快照                                    | EVS ReadOnlyAccess                                | EVS FullAccess                                   |
| 项目                                          | EPS ReadOnlyAccess                                | EPS FullAccess                                   |
| 镜像                                          | IMS ReadOnlyAccess                                | IMS FullAccess                                   |
| Vpc, Vpc对等连接, 路由表, 弹性网卡,EIP,安全组 | VPC ReadOnlyAccess                                | VPC FullAccess                                   |
| NAT                                           | NAT ReadOnlyAccess                                | NAT FullAccess                                   |
| 对象存储                                      | OBS ReadOnlyAccess                                | OBS Administrator                                |
| 负载均衡                                      | ELB ReadOnlyAccess                                | ELB FullAccess                                   |
| RDS                                           | RDS ReadOnlyAccess                                | RDS FullAccess                                   |
| 弹性缓存                                      | DCS ReadOnlyAccess                                | DCS FullAccess                                   |
| 操作日志                                      | CTS ReadOnlyAccess                                | CTS FullAccess                                   |
| NAS                                           | SFS ReadOnlyAccess<br>SFS Turbo ReadOnlyAccess    | SFS FullAccess<br>SFS Turbo FullAccess           |
| WAF                                           | WAF ReadOnlyAccess                                | WAF FullAccess                                   |
| IAM                                           | IAM ReadOnlyAccess                                | Security Administrator                           |
| DNS                                           | DNS ReadOnlyAccess                                | DNS FullAccess                                   |
| 账单,余额,费用                                | BSS Operator                                      | BSS Administrator                                |
| 监控                                          | CES ReadOnlyAccess                                | CES FullAccess                                   |

##### 如何获取账单存储桶URL？

**新版**

1. 登录华为云平台，单击顶部 **_"费用中心-费用账单"_** 菜单项，进入费用中心页面。
    ![](../../../../faq/image/huaweinewconsum.png)

2. 单击左侧[总览]菜单，在总览页面的右侧部分“账单数据存储”中查看并记录对象存储名称，如未配置，需要在该页面启用账单数据存储，并配置存储的OBS桶并进行授权验证操作等，设置完成后，每天的增量账单数据将同步存储到对应的OBS上。建议该bucket中仅存放账单文件。

    ![](../../../../faq/image/huaweinewbillingbucket.png)

3. 在华为云控制台的对象存储服务(OBS)中查看对应存储桶的概览信息，获取访问域名即为存储桶URL。

    ![](../../../../faq/image/huaweibillingbucketurl.png) 

**旧版**

1. 登录华为云平台，单击顶部[更多]菜单的下拉菜单 **_"费用-消费总览"_** 菜单项，进入费用中心页面。
   ![](../../../../faq/image/huaweiconsum.png)

2. 单击左侧菜单[消费数据存储]，在进入的消费数据存储中查看并记录对象存储桶名称，如未配置，需要在该页面设置存储桶并进行授权验证操作等，设置完成后，每天的增量账单数据将同步存储到对应的OSS上。建议该bucket中仅存放账单文件。
   ![](../../../../faq/image/huaweibillingbucket.png)

3. 在华为云控制台的对象存储服务(OBS)中查看对应存储桶的概览信息，获取访问域名即为存储桶URL。
   ![](../../../../faq/image/huaweibillingbucketurl.png) 

### 新建腾讯云账号

1. 在云账号页面单击列表上方 **_"新建"_** 按钮，进入新建云账号页面。
2. 选择云平台为腾讯云，单击 **_"下一步：配置云账号"_** 按钮，进入配置云账号页面。
3. 配置以下参数：
   - 名称：腾讯云平台的名称。
   - APP ID/密钥ID/密码：腾讯云账号的APP ID与账号ID有唯一对应关系。对接腾讯云平台的APP ID/密钥ID/密码。具体请参考[腾讯云相关参数获取方式](#腾讯云相关参数获取方式)。
   - 域：选择云账号所属的域。当云账号私有状态下，域下所有项目用户都可以使用云账号创建资源。
   - 资源归属项目：选择将云账号上的资源同步到{{<oem_name>}}平台的本地项目。如需将云账号上的资源按照云上项目归类，请先指定默认资源归属项目，并勾选自动创建项目。勾选后，将会在{{<oem_name>}}平台创建与云上项目同名的本地项目，并将资源同步到对应项目中。云上没有项目归属的资源将会同步到默认资源归属项目。
   - 代理：当云账号需要代理才可以正常访问时设置该项，留空代表直连。如没有合适的代理，直接单击“新建”超链接，在弹出的新建代理对话框中设置相关参数，创建代理。
   - 开启免密登录：启用该项后，会自动将系统的SAML信息同步到云账号上，并成为云上登录的身份提供商。实现通过本系统单点登录到公有云平台。
   - 自动同步：设置是否自动同步腾讯云平台上的信息，并设置自动同步的时间间隔。
   - 共享范围：设置云账号的共享范围，默认为不共享，则仅云账号所在域可以使用该账号，若设置为全局共享，则平台上所有用户都可以使用该云账号创建资源。
4. 单击 **_"连接测试"_** 按钮，测试输入的参数是否正确。
5. 测试成功后，单击 **_"下一步：配置同步资源区域"_** 按钮，进入配置同步资源区域页面，该配置可在云账号详情页-订阅-区域进行修改（默认同步所有区域）。如在{{<oem_name>}}平台默认同步所有区域，可直接单击 **_"跳过"_** 按钮。
6. 配置成功后，单击  **_"下一步：账单文件访问信息（可选）"_** 按钮，进入账单文件访问信息页面配置云账号的账单参数以便用户可以在费用中查看云账号的账单信息。账单文件访问信息页面选填，如不需要在{{<oem_name>}}平台查看云账号账单信息，可直接单击 **_跳过_** 按钮。如需要在{{<oem_name>}}平台中查看账单信息等，请配置相关参数，配置完成且测试成功后，单击 **_"确定"_** 按钮，并进入定时同步任务设置页面配置云账号的同步任务使得云账号自动同步行为更加可控。
7. 腾讯云账单通过API获取，因此在该页面只需要配置以下参数。
   - 立即采集账单：{{<oem_name>}}平台默认每天凌晨4点自动采集账单。开启该项后，配置完账单文件访问信息后，将会立即采集账单。
   - 时间范围：当启用立即采集账单后，支持设置时间范围，立即采集时间范围内的账单，请确保在选择的时间范围内有账单数据。建议采集1~6个月内的账单，否则会因为数据太多，造成系统压力多大影响日常采集账单的任务。
8. 定时同步任务设置页面选填，如不需要在{{<oem_name>}}平台设置自动同步任务，可直接单击 **_"跳过"_** 按钮。如需要在{{<oem_name>}}平台中设置云账号自动同步的时间，请配置相关参数，配置完成且测试通过后，单击 **_"确定"_** 按钮，创建腾讯云账号。



#### 腾讯云相关参数获取方式

##### 如何获取腾讯云API密钥

1. 登录腾讯云控制台，单击右上角 **_"云产品"_** 菜单项，在展开的菜单中搜索 **_"云API密钥"_** 菜单项，单击进入API密钥管理页面。
   ![](../../../../faq/image/faq_account_qcloud_1.png)

2. 在API密钥管理页面获取APP ID、密钥ID（SecretId）、密码（SecretKey）对应的值。
   ![](../../../../faq/image/faq_account_qcloud_2.png)

##### 通过平台管理腾讯云资源，需要云账号具备哪些权限

| 功能                                          | 只读权限                                                                                                          | 可读可写权限                                                                                      |
| :----------                                   | :--------                                                                                                         | :----------                                                                                       |
| 所有功能总和                                  | ReadOnlyAccess                                                                                                    | AdministratorAccess                                                                               |
| 虚拟机, 安全组, 镜像, 磁盘, 快照              | QcloudCVMReadOnlyAccess                                                                                           | QcloudCVMFullAccess                                                                               |
| Vpc, Vpc对等连接, 路由表, NAT, 弹性网卡       | QcloudVPCReadOnlyAccess                                                                                           | QcloudVPCFullAccess                                                                               |
| Eip                                           | -                                                                                                                 | QcloudEIPFullAccess                                                                               |
| 对象存储                                      | QcloudCOSReadOnlyAccess                                                                                           | QcloudCOSFullAccess                                                                               |
| 负载均衡                                      | QcloudCLBReadOnlyAccess                                                                                           | QcloudCLBFullAccess                                                                               |
| RDS                                           | QcloudMariaDBReadOnlyAccess<br>QcloudCDBReadOnlyAccess<br>QcloudSQLServerReadOnlyAccess<br>QcloudPostgreSQLReadOnlyAccess  | QcloudMariaDBFullAccess<br>QcloudCDBFullAccess<br>QcloudSQLServerFullAccess<br>QcloudPostgreSQLFullAccess  |
| 弹性缓存                                      | QcloudRedisReadOnlyAccess                                                                                         | QcloudRedisFullAccess                                                                             |
| 操作日志                                      | QcloudAuditReadOnlyAccess                                                                                         | QcloudAuditFullAccess                                                                             |
| NAS                                           | -                                                                                                                 | -                                                                                                 |
| WAF                                           | -                                                                                                                 | -                                                                                                 |
| IAM                                           | QcloudCamReadOnlyAccess                                                                                           | QcloudCamFullAccess                                                                               |
| DNS                                           | QcloudDNSPodReadOnlyAccess<br>QcloudPrivateDNSReadOnlyAccess                                                         | QcloudPrivateDNSFullAccess<br>QcloudDNSPodFullAccess                                                 |
| 账单,余额,费用                                | -                                                                                                                 | QCloudFinanceFullAccess                                                                           |
| 监控                                          | QcloudMonitorReadOnlyAccess                                                                                       | QcloudMonitorFullAccess                                                                           |

### 新建UCloud账号

1. 在公有云账号页面单击列表上方 **_"新建"_** 按钮，，进入新建云账号页面。
2. 选择云平台为UCloud，单击 **_"下一步：配置云账号"_** 按钮，进入配置云账号页面。
3. 配置以下参数：
   - 名称：UCloud平台的名称。
   - 公钥/私钥：获取方式具体请参考[UCloud相关参数获取方式](#ucloud相关参数获取方式)。
   - project_id：当使用UCloud子账号时，必须配置该项。使用主账号时无需配置该项。
   - 域：选择云账号所属的域。当云账号私有状态下，域下所有项目用户都可以使用云账号创建资源。
   - 资源归属项目：选择将云账号上的资源同步到{{<oem_name>}}平台的本地项目。如需将云账号上的资源按照云上项目归类，请先指定默认资源归属项目，并勾选自动创建项目。勾选后，将会在{{<oem_name>}}平台创建与云上项目同名的本地项目，并将资源同步到对应项目中。云上没有项目归属的资源将会同步到默认资源归属项目。
   - 代理：当云账号需要代理才可以正常访问时设置该项，留空代表直连。如没有合适的代理，直接单击“新建”超链接，在弹出的新建代理对话框中设置相关参数，创建代理。
   - 自动同步：设置是否自动同步UCloud平台上的信息，并设置自动同步的时间间隔。
4. 单击 **_"连接测试"_** 按钮，测试输入的参数是否正确。
5. 测试成功后，单击 **_"下一步：配置同步资源区域"_** 按钮，进入配置同步资源区域页面，该配置可在云账号详情页-订阅-区域进行修改（默认同步所有区域）。如在{{<oem_name>}}平台默认同步所有区域，可直接单击 **_"跳过"_** 按钮，并进入定时同步任务设置页面配置云账号的同步任务使得云账号自动同步行为更加可控。
6. 定时同步任务设置页面选填，如不需要在{{<oem_name>}}平台设置自动同步任务，可直接单击 **_"跳过"_** 按钮。如需要在{{<oem_name>}}平台中设置云账号自动同步的时间，请配置相关参数，配置完成且测试成功后，单击 **_"确定"_** 按钮，创建UCloud账号。

#### UCloud相关参数获取方式

##### 如何获取 UCloud API 密钥

1. 登录 UCloud 控制台，单击顶部 **_"全部产品"_** ，搜索或选择 **_"开放API UAPI"_** 菜单项 ，进入 API 产品页面；
    
    ![](../../../../faq/image/ucloudapi.png)

2. 单击“API密钥”页签，进入API 密钥页面。单击 **_"显示"_** 按钮，进行手机短信二次验证；

    ![](../../../../faq/image/ucloudapikeyshow.png)

3. 通过手机验证后获取公钥和私钥值。

    ![](../../../../faq/image/ucloudapikeypair.png)

4. 若使用子账号，除获取公钥或私钥外，还需要获取project_id，在“访问控制-用户管理-子账户详情”中获取project_id为个人权限中的应用项目的项目ID。

    ![](../../../../faq/image/ucloudprojectid.png)


##### 使用平台管理UCloud资源，需要云账号具备哪些权限

| 权限策略            | 策略说明                        |
| :------------------ | :---------------------- |
| AdministratorAccess | 超级管理员权限 |

### 新建Google账号

{{% alert title="注意" color="warning" %}}
- 请确保{{<oem_name>}}平台与谷歌云网络互通。
- 如{{<oem_name>}}平台与谷歌云网络不通，可通过配置代理访问谷歌云。
{{% /alert %}}

1. 在云账号页面单击列表上方 **_"新建"_** 按钮，进入新建云账号页面。
2. 选择云平台为“Google”，单击 **_"下一步：配置云账号"_** 按钮，进入配置云账号页面。
3. 配置以下参数：
   - 名称：谷歌云的云账号名称。
   - project_id、private_key_id、private_key、client_email等参数具体可参考[Google相关参数获取方式](#google相关参数获取方式)。
   - 域：选择云账号所属的域。当云账号私有状态下，域下所有项目用户都可以使用云账号创建资源。
   - 资源归属项目：选择将云账号上的资源同步到{{<oem_name>}}平台的本地项目。如需将云账号上的资源按照云上项目归类，请先指定默认资源归属项目，并勾选自动创建项目。勾选后，将会在{{<oem_name>}}平台创建与云上项目同名的本地项目，并将资源同步到对应项目中。云上没有项目归属的资源将会同步到默认资源归属项目。
   - 代理：当云账号需要代理才可以正常访问时设置该项，留空代表直连。如没有合适的代理，直接单击“新建”超链接，在弹出的新建代理对话框中设置相关参数，创建代理。
   - 自动同步：设置是否自动同步Google平台上的信息，并设置自动同步的时间间隔。
   - 共享范围：设置云账号的共享范围，默认为不共享，则仅云账号所在域可以使用该账号，若设置为全局共享，则平台上所有用户都可以使用该云账号创建资源。
4. 单击 **_"连接测试"_** 按钮，测试输入的参数是否正确。
5. 测试成功后，单击 **_"下一步：配置同步资源区域"_** 按钮，进入配置同步资源区域页面，该配置可在云账号详情页-订阅-区域进行修改（默认同步所有区域）。如在{{<oem_name>}}平台默认同步所有区域，可直接单击 **_"跳过"_** 按钮。
6. 配置成功后，单击  **_"下一步：账单文件访问信息（可选）"_** 按钮，进入账单文件访问信息页面配置云账号的账单参数以便用户可以在费用中查看云账号的账单信息。账单文件访问信息页面选填，如不需要在{{<oem_name>}}平台查看云账号账单信息，可直接单击 **_跳过_** 按钮。如需要在{{<oem_name>}}平台中查看账单信息等，请配置相关参数，配置完成且测试成功后，单击 **_"确定"_** 按钮，并进入定时同步任务设置页面配置云账号的同步任务使得云账号自动同步行为更加可控。
   - 账单数据源：选择Google账单的存放路径，包括Bigquery和bucket两种，目前Google账单已不再支持bucket。
   - 当账单数据源选择“Bigquery”时，需要配置以下参数：
       - 云账号类型：包括主账号和关联账号，使用关联账号之前请确保主账号已导入{{<oem_name>}}平台，并在使用关联账号时选择该主账号。
       - Bigquery表ID：存储Google账单的数据集的表ID，具体请参考[如何在谷歌云平台配置并获取Bigquery配置信息?](#如何在谷歌云平台配置并获取bigquery配置信息)。
       - 账单分析范围：设置平台分析云账号账单的范围。目前仅支持本平台纳管账号。
           - 本平台纳管账号：即采集主账号及主账号关联的子账号的账单信息。如该主账号仅作为其他账号的付款账号时，采集到的其他账号的账单文件将会被丢弃。
   - 当账单数据源选择“Bucket”时，需要配置以下参数：
       - 云账号类型：包括主账号和关联账号，使用关联账号之前请确保主账号已导入{{<oem_name>}}平台，并在使用关联账号时选择该主账号。
       - 账单文件/存储桶URL：账单文件所在存储桶的URL。具体请参考[如何获取账单文件的存储桶URL以及文件前缀？](#如何获取账单文件的存储桶url以及文件前缀)。
       - 账单文件/文件前缀：即为文件导出的报告前缀信息。当账单bucket中除账单文件外还存放了其他文件时，需要配置文件前缀仅获取bucket中的账单文件等。
       - 账单分析范围：设置平台分析云账号账单的范围。目前仅支持本平台纳管账号。
           - 本平台纳管账号：即采集主账号及主账号关联的子账号的账单信息。如该主账号仅作为其他账号的付款账号时，采集到的其他账号的账单文件将会被丢弃。
       - 使用量文件/存储桶URL：即使用量所在存储桶的URL。具体请参考[如何获取使用量文件存储桶URL和文件前缀？](#如何获取账单文件的存储桶url以及文件前缀)。
       - 使用量文件/文件前缀：即为设置页面的报告前缀信息。当使用量bucket中除使用量文件外还存放了其他文件时，需要配置文件前缀仅获取bucket中的使用量文件等。
   - 立即采集账单：{{<oem_name>}}平台默认每天凌晨4点自动采集账单。开启该项后，配置完账单文件访问信息后，将会立即采集账单。
   - 时间范围：当启用立即采集账单后，支持设置时间范围，立即采集时间范围内的账单，请确保在选择的时间范围内有账单数据。建议采集1~6个月内的账单，否则会因为数据太多，造成系统压力多大影响日常采集账单的任务。
7. 定时同步任务设置页面选填，如不需要在{{<oem_name>}}平台设置自动同步任务，可直接单击 **_"跳过"_** 按钮。如需要在{{<oem_name>}}平台中设置云账号自动同步的时间，请配置相关参数，配置完成且测试成功后，单击 **_"确定"_** 按钮，创建谷歌云账号

#### Google相关参数获取方式

##### 如何获取谷歌云服务帐号密钥信息？

**纳管指定项目**

1. 打开“[GCP Console中的IAM和管理-IAM页面](https://console.cloud.google.com/project/_/iam-admin)”页面并登录。

    ![](../../../../faq/image/google_iam.png)

2. 单击顶部“选择项目”，选择需要授权的项目。
 
    ![](../../../../faq/image/google_project.png)

3. 在左侧导航栏中选择“服务账号”，进入指定项目的服务账号页面。
4. 单击 **_"创建服务账号"_** 按钮，进入创建服务账号页面。
5. 配置服务账号名称、服务账号ID、服务账号说明等，单击 **_"创建"_** 按钮，创建服务账号并向此服务帐号授予对项目的访问权限。

    ![](../../../../faq/image/google_createserviceaccount.png)

6. 选择Project-Owner或Project-Viewer角色，Owner代表对项目的管理权限，Viewer代表对项目的只读权限，如需云管平台对Google云账号资源进行管理操作，请选择Project-Owner角色，单击 **_"继续"_** 按钮。

    ![](../../../../faq/image/google_serviceaccountpolicy.png)

7. 向用户授予访问此服务帐号的权限 (可选)步骤对云管平台无影响，请用户根据需求设置，配置完成后，单击 **_"继续"_** 按钮。

8. 在服务账号页面，单击新创建的服务账号右侧操作列![colum](../../../../faq/image/colum.png)按钮，单击 **_"创建密钥"_** 菜单项。
 
    ![](../../../../faq/image/google_serviceaccount1.png) 

9. 选择密钥类型为“JSON”，单击 **_"创建"_** 按钮，下载json格式的密钥文件，内容如下，分别获取project_id、private_key_id、private_key、client_email等内容。

    ![](../../../../faq/image/google_create.png) 

    ```bash
    {
     "type": "service_account",
     "project_id": "[PROJECT-ID]",
     "private_key_id": "[KEY-ID]",
     "private_key": "-----BEGIN PRIVATE KEY-----\n[PRIVATE-KEY]\n-----END PRIVATE KEY-----\n",
     "client_email": "[SERVICE-ACCOUNT-EMAIL]",
     "client_id": "[CLIENT-ID]",
     "auth_uri": "https://accounts.google.com/o/oauth2/auth",
     "token_uri": "https://accounts.google.com/o/oauth2/token",
     "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
     "client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/[SERVICE-ACCOUNT-EMAIL]"
     }
    ```

**纳管多个项目**

如需要使用上面获取的服务账户的密钥纳管多个项目，可按照以下步骤进行设置。

1. 打开“[GCP Console中的IAM和管理-IAM页面](https://console.cloud.google.com/project/_/iam-admin)”页面，选择其他需要纳管的项目。
2. 单击顶部 **_"添加"_** 按钮，在新成员中添加上面步骤创建的服务账号，并设置角色为Project-Owner或Project-Viewer，Owner代表对项目的管理权限，Viewer代表对项目的只读权限，如需云管平台对Google云账号资源进行管理操作，请选择Project-Owner角色，单击 **_"保存"_** 按钮。

    ![](../../../../faq/image/google_serviceaccount_otherproject.png)

3. 重复上面的步骤，纳管更多项目。

##### 启用相关API

{{% alert title="说明" %}}
谷歌云的API具有项目属性，当需要纳管谷歌云上多个项目时，需要分别在每个项目中启用相关API。
{{% /alert %}}

**{{<oem_name>}}管理谷歌云需要启用API**：

获取密钥文件后，还需要在Google API库中启用授权项目中的项目资源管理API（Cloud Resource Manager API）和自定义镜像创建机器API（Cloud Build API）。启用API后，用户可在{{<oem_name>}}平台管理使用谷歌云。
  
1. 在API库的[Cloud Resource Manager API](https://console.developers.google.com/apis/library/cloudresourcemanager.googleapis.com)页面中启用授权项目的Cloud Resource Manager API。可通过顶部切换授权项目。
   ![](../../../../faq/image/cloudresourcemanagerapi.png)
         
2. 在API库的[Cloud Build API](https://console.developers.google.com/apis/library/cloudbuild.googleapis.com )页面中启用授权项目的Cloud Build API。可通过顶部切换授权项目。
   ![](../../../../faq/image/cloudbuildapi.png)

**{{<oem_name>}}管理谷歌云RDS需要启用API**：

1. 在API库的[Cloud SQL Admin API](https://console.developers.google.com/apis/library/sqladmin.googleapis.com)页面中启用Cloud SQL Admin API。可通过顶部切换授权项目。
   ![](../../../../faq/image/cloudsqladminapi.png)

##### 通过平台管理Google云资源，需要云账号具备哪些权限

| 功能                                                      | 只读权限                                              | 可读可写权限                     |
| :----------                                               | :--------                                             | :----------                      |
| 所有功能总和                                              | Viewer                                                | Editor                           |
| 虚拟机, 磁盘, 安全组, 镜像, 快照, 磁盘, 镜像, 负载均衡    | Compute Viewer                                        | Compute Editor                   |
| 项目                                                      | -                                                     | -                                |
| Vpc, Vpc对等连接, 路由表, NAT, 弹性网卡,EIP, NAT          | Compute Network Viewer                                | Compute Network Admin            |
| 对象存储                                                  | Storage Legacy Bucket Reader<br>Storage Object Viewer | Storage Admin                    |
| RDS                                                       | Cloud SQL Viewer                                      | Cloud SQL Admin                  |
| 弹性缓存                                                  | Redis Enterprise Cloud Viewer                         | Redis Enterprise Cloud Admin     |
| 操作日志                                                  | Logs Viewer                                           | Logging Admin                    |
| NAS                                                       | Cloud Filestore Viewer                                | Cloud Filestore Editor           |
| WAF                                                       | -                                                     | -                                |
| IAM                                                       | Role Viewer                                           | Role Administrator               |
| DNS                                                       | DNS Reader                                            | DNS Administrator                |
| 账单,费用                                                 | Billing Account Viewer                                | Billing Account Administrator    |
| 监控                                                      | Monitoring Viewer                                     | Monitoring Admin                 |

##### 如何在谷歌云平台配置并获取Bigquery配置信息?

1. 登录谷歌云控制台，单击左侧菜单 **_"结算"_** 菜单项，进入结算页面。
   ![](../../../../faq/image/googlebilling.png)

2. 单击左侧菜单[结算导出]，在BIGQUERY EXPORT页签下，启用详细使用费，并配置项目和数据集名称。

    ![](../../../../faq/image/googlebigqueryconfig.png)

3. 单击数据集名称，跳转到Bigquery，展开右侧节点，选中数据集名称下的分区表，在进入的页面中单击顶部“详情”页签，获取表ID信息。

    ![](../../../../faq/image/gcpbigquerytableid.png)

4. 在表详情页面，单击右上角 **_"修改详情"_** 按钮，将有效期设置为None。若设置有效期则会从bigquery中清理过期的数据，请谨慎设置。

    ![](../../../../faq/image/gcomodifytable.png)

##### 如何获取账单文件的存储桶URL以及文件前缀？

1. 登录谷歌云控制台，单击左侧菜单 **_"结算"_** 菜单项，进入结算页面。
   ![](../../../../faq/image/googlebilling.png)

2. 单击左侧菜单[结算导出]，在进入的账单页面中单击“文件导出”页签，查看并记录存储分区名称以及报告前缀的信息。其中报告前缀即文件前缀。如果未设置，需要在该页面配置存储分区名称和报告前缀信息等，设置完成后，每天的增量账单数据将同步存储到对应的存储上。建议该bucket中仅存放账单文件。
   ![](../../../../faq/image/googlebillingbucket.png)
    
3. 单击左侧菜单[Storage/浏览器]，在进入的存储页面中单击对应存储分区名称，并单击“概览”页签，查看存储分区的概览信息，其中链接网址为存储桶URL。
   ![](../../../../faq/image/googlebillingbucketurl.png) 

4. 当账单bucket中除账单文件外还存放了其他文件时，需要配置文件前缀仅获取bucket中的账单文件等。

##### 如何获取使用量文件存储桶URL和文件前缀？

1. 在谷歌云控制台中单击左侧菜单[Compute Engine/设置]，进入设置页面。</br>
   ![](../../../../faq/image/googleusagesetting.png)

2. 请确保已勾选“启用使用情况导出功能”，并记录存储分区名称和报告前缀信息，其中报告前缀即文件前缀。如未配置，需要勾选“启用使用情况导出功能”，并配置存储分区等。
   ![](../../../../faq/image/googleusagebucket.png) 

3. 单击左侧菜单[Storage/浏览器]，在进入的存储页面中单击对应存储分区名称，并单击“概览”页签，查看存储分区的概览信息，其中链接网址为存储桶URL。
   ![](../../../../faq/image/googleusagebucketurl.png)

4. 当使用量bucket中除使用量文件外还存放了其他文件时，需要配置文件前缀仅获取bucket中的使用量文件等。


### 新建天翼云账号

1. 在云账号页面单击列表上方 **_"新建"_** 按钮，进入新建云账号页面。
2. 选择云平台为“天翼云”，单击 **_"下一步：配置云账号"_** 按钮，进入配置云账号页面。
3. 配置以下参数：
   - 名称：天翼云的云账号名称。 
   - 账号类型：目前支持对接全球区和中国区的天翼云账号。
   - 密钥ID、密码获取方式：目前无法直接使用天翼云官网界面上申请的密钥信息，需要用户联系天翼云技术支持获取Access Key Id和Secret Access Key信息，并需要在天翼云上配置ip白名单。如用户不清楚如何获取，可直接联系运维人员寻求帮助。  
   - 域：选择云账号所属的域。当云账号私有状态下，域下所有项目用户都可以使用云账号创建资源。
   - 资源归属项目：选择将云账号上的资源同步到{{<oem_name>}}平台的本地项目。如需将云账号上的资源按照云上项目归类，请先指定默认资源归属项目，并勾选自动创建项目。勾选后，将会在{{<oem_name>}}平台创建与云上项目同名的本地项目，并将资源同步到对应项目中。云上没有项目归属的资源将会同步到默认资源归属项目。
   - 代理：当云账号需要代理才可以正常访问时设置该项，留空代表直连。如没有合适的代理，直接单击“新建”超链接，在弹出的新建代理对话框中设置相关参数，创建代理。
   - 自动同步：设置是否自动同步天翼云平台上的信息，并设置自动同步的时间间隔。
   - 共享范围：设置云账号的共享范围，默认为不共享，则仅云账号所在域可以使用该账号，若设置为全局共享，则平台上所有用户都可以使用该云账号创建资源。
4. 单击 **_"连接测试"_** 按钮，测试输入的参数是否正确。
5. 测试成功后，单击 **_"下一步：配置同步资源区域"_** 按钮，进入配置同步资源区域页面，该配置可在云账号详情页-订阅-区域进行修改（默认同步所有区域）。如在{{<oem_name>}}平台默认同步所有区域，可直接单击 **_"跳过"_** 按钮，并进入定时同步任务设置页面配置云账号的同步任务使得云账号自动同步行为更加可控。
6. 定时同步任务设置页面选填，如不需要在{{<oem_name>}}平台设置自动同步任务，可直接单击 **_"跳过"_** 按钮。如需要在{{<oem_name>}}平台中设置云账号自动同步的时间，请配置相关参数，配置完成且测试成功后，单击 **_"确定"_** 按钮，创建天翼云账号。

### 新建移动云账号

目前仅支持同步移动云账号上的资源，不支持操作资源。

1. 在云账号页面单击列表上方 **_"新建"_** 按钮，进入新建云账号页面。
2. 选择云平台为“移动云”，单击 **_"下一步：配置云账号"_** 按钮，进入配置云账号页面。
3. 配置以下参数：
    - 名称：移动云的云账号名称。
    - 密钥ID、密码：获取方式具体请参考[移动云相关参数获取方式](#移动云相关参数获取方式)。
    - 域：选择云账号所属的域。当云账号私有状态下，域下所有项目用户都可以使用云账号创建资源。
    - 资源归属项目：选择将云账号上的资源同步到{{<oem_name>}}平台的本地项目。如需将云账号上的资源按照云上项目归类，请先指定默认资源归属项目，并勾选自动创建项目。勾选后，将会在{{<oem_name>}}平台创建与云上项目同名的本地项目，并将资源同步到对应项目中。云上没有项目归属的资源将会同步到默认资源归属项目。
    - 代理：当云账号需要代理才可以正常访问时设置该项，留空代表直连。如没有合适的代理，直接单击“新建”超链接，在弹出的新建代理对话框中设置相关参数，创建代理。
    - 自动同步：设置是否自动同步天翼云平台上的信息，并设置自动同步的时间间隔。
    - 共享范围：设置云账号的共享范围，默认为不共享，则仅云账号所在域可以使用该账号，若设置为全局共享，则平台上所有用户都可以使用该云账号创建资源。
4. 单击 **_"连接测试"_** 按钮，测试输入的参数是否正确。
5. 测试成功后，击 **_"下一步：配置同步资源区域"_** 按钮，进入配置同步资源区域页面，该配置可在云账号详情页-订阅-区域进行修改（默认同步所有区域）。如在{{<oem_name>}}平台默认同步所有区域，可直接单击 **_"跳过"_** 按钮。并进入定时同步任务设置页面配置云账号的同步任务使得云账号自动同步行为更加可控。
6. 定时同步任务设置页面选填，如不需要在{{<oem_name>}}平台设置自动同步任务，可直接单击 **_"跳过"_** 按钮。如需要在{{<oem_name>}}平台中设置云账号自动同步的时间，请配置相关参数，配置完成且测试成功后，单击 **_"确定"_** 按钮，创建移动云账号。
 

#### 移动云相关参数获取方式

##### 如何获取移动云的 API 密钥？

1. 登录移动云控制台，在所有产品中搜索“AK管理”，进入AccessKey管理页面。

    ![](../../../../faq/image/ecloud.png)

2. 在AccessKey管理页面创建密钥或查看已有密钥的Access key和Secret key。

    ![](../../../../faq/image/ecloudaccesskey.png)

##### 管理移动云资源，需要云账号具备哪些权限

| 权限策略            | 策略说明                        |
| :------------------ | :---------------------- |
| Admin| 管理员角色 |

### 新建京东云账号

目前仅支持同步京东云账号上的资源，不支持操作资源。

1. 在云账号页面单击列表上方 **_"新建"_** 按钮，进入新建云账号页面。
2. 选择云平台为“京东云”，单击 **_"下一步：配置云账号"_** 按钮，进入配置云账号页面。
3. 配置以下参数：
    - 名称：京东云的云账号名称。
    - 密钥ID、密码：获取方式具体请参考[京东相关参数获取方式](#京东云相关参数获取方式)。
    - 域：选择云账号所属的域。当云账号私有状态下，域下所有项目用户都可以使用云账号创建资源。
    - 资源归属项目：选择将云账号上的资源同步到{{<oem_name>}}平台的本地项目。如需将云账号上的资源按照云上项目归类，请先指定默认资源归属项目，并勾选自动创建项目。勾选后，将会在{{<oem_name>}}平台创建与云上项目同名的本地项目，并将资源同步到对应项目中。云上没有项目归属的资源将会同步到默认资源归属项目。
    - 代理：当云账号需要代理才可以正常访问时设置该项，留空代表直连。如没有合适的代理，直接单击“新建”超链接，在弹出的新建代理对话框中设置相关参数，创建代理。
    - 自动同步：设置是否自动同步京东平台上的信息，并设置自动同步的时间间隔。
    - 共享范围：设置云账号的共享范围，默认为不共享，则仅云账号所在域可以使用该账号，若设置为全局共享，则平台上所有用户都可以使用该云账号创建资源。
4. 单击 **_"连接测试"_** 按钮，测试输入的参数是否正确。
5. 测试成功后，单击 **_"下一步：配置同步资源区域"_** 按钮，进入配置同步资源区域页面，该配置可在云账号详情页-订阅-区域进行修改（默认同步所有区域）。如在{{<oem_name>}}平台默认同步所有区域，可直接单击 **_"跳过"_** 按钮。
6. 配置成功后，单击  **_"下一步：账单文件访问信息（可选）"_** 按钮，进入账单文件访问信息页面配置云账号的账单参数以便用户可以在费用中查看云账号的账单信息。账单文件访问信息页面选填，如不需要在{{<oem_name>}}平台查看云账号账单信息，可直接单击 **_跳过_** 按钮。如需要在{{<oem_name>}}平台中查看账单信息等，请配置相关参数，配置完成且测试成功后，单击 **_"确定"_** 按钮。 并进入定时同步任务设置页面配置云账号的同步任务使得云账号自动同步行为更加可控。
7. 京东云账单通过API获取，因此在该页面只需要配置以下参数。
   - 立即采集账单：{{<oem_name>}}平台默认每天凌晨4点自动采集账单。开启该项后，配置完账单文件访问信息后，将会立即采集账单。
   - 时间范围：当启用立即采集账单后，支持设置时间范围，立即采集时间范围内的账单，请确保在选择的时间范围内有账单数据。建议采集1~6个月内的账单，否则会因为数据太多，造成系统压力多大影响日常采集账单的任务。
8. 定时同步任务设置页面选填，如不需要在{{<oem_name>}}平台设置自动同步任务，可直接单击 **_"跳过"_** 按钮。如需要在{{<oem_name>}}平台中设置云账号自动同步的时间，请配置相关参数，配置完成且测试成功后，单击 **_"确定"_** 按钮，创建京东云账号并采集账单。
#### 京东云相关参数获取方式

##### 如何获取京东云的API密钥

1. 登录京东云控制台，鼠标悬停在右上角用户名处，选择下拉菜单 **_"Access Key管理"_** 菜单项，进入Access Key管理页面。

    ![](../../../../faq/image/jdak.png)

2. 查看已有Access Key信息，或单击 **_"新建"_** 按钮，新建Access Key，单击 **_"查看"_** 按钮，获取Access Key Secret信息。

    ![](../../../../faq/image/jdaksk.png)

### 新建VMware账号

**支持版本**

支持纳管VMware 5.0~7.0版本。

**VMware资源纳管流程**

1. 新建VMware云账号，自动在{{<oem_name>}}平台创建二层网络和IP子网，VMware网络与{{<oem_name>}}平台二层网络和IP子网的对应关系如下：
    - 一个vSwitch或Distributed vSwitch对应一个二层网络；
    - 同一个二层网络下具体相同VLAN的连续IP地址段为一个IP子网；
2. VMware云账号添加完成后，如自动添加的二层网络和IP子网不符合组网需求，请根据VMware的实际网络环境进行合并wire和合并IP子网的操作；合并wire操作不可逆，如配置错误，请删除云账号后重新添加。

**操作步骤**

1. 在云账号页面单击列表上方 **_"新建"_** 按钮，进入新建云账号页面。
2. 选择云平台为VMware，单击 **_"下一步：配置云账号"_** 按钮，进入配置云账号页面。
3. 配置以下参数：  
   - 名称：VMware账号的名称。
   - vCenter地址：vCenter服务器的域名或IP地址。
   - 端口号：默认为443。
   - 账号：vCenter的管理员用户名。
   - 密码：vCenter管理员用户的密码。
   - 域：选择云账号所属的域。当云账号私有状态下，域下所有项目用户都可以使用云账号创建资源。
   - 资源归属项目：选择将云账号上的资源同步到{{<oem_name>}}平台的本地项目。如需将云账号上的资源按照云上项目归类，请先指定默认资源归属项目，并勾选自动创建项目。勾选后，将会在{{<oem_name>}}平台创建与云上项目同名的本地项目，并将资源同步到对应项目中。云上没有项目归属的资源将会同步到默认资源归属项目。
   - 代理：当云账号需要代理才可以正常访问时设置该项，留空代表直连。如没有合适的代理，直接单击“新建”超链接，在弹出的新建代理对话框中设置相关参数，创建代理。
   - 自动同步：设置是否自动同步vCenter上信息，若启用需要设置自动同步的时间间隔。
   - 共享范围：设置云账号的共享范围，默认为不共享，则仅云账号所在域可以使用该账号，若设置为全局共享，则平台上所有用户都可以使用该云账号创建资源。
4. 单击 **_"连接测试"_** 按钮，测试输入的参数是否正确。
5. 测试成功后，单击 **_"下一步：定时同步任务设置（可选）"_** 按钮，进入定时同步任务设置页面配置云账号的同步任务使得云账号自动同步行为更加可控。定时同步任务设置页面选填，如不需要在{{<oem_name>}}平台设置自动同步任务，可直接单击 **_"跳过"_** 按钮。如需要在{{<oem_name>}}平台中设置云账号自动同步的时间，请配置相关参数，配置完成且测试成功后，单击 **_"确定"_** 按钮，开始创建VMware云账号、相关IP子网，并开始同步云账号上的资源。

### 新建OpenStack账号

**支持版本**

支持纳管OpenStack M版及之后版本。

**注意事项**

如果纳管的OpenStack平台认证地址是域名时，还需要在控制节点上配置域名解析，否则会因为无法解析域名导致无法同步OpenStack平台的资源。

步骤如下：

```bash
# 修改coredns的configmap
$ kubectl edit cm -n kube-system coredns

   Corefile: |
       .:53 {
           errors
           health
           kubernetes cluster.local in-addr.arpa ip6.arpa {
              pods insecure
              upstream
              fallthrough in-addr.arpa ip6.arpa
              ttl 30
           }
           hosts {
               192.168.1.2 domain

               fallthrough
           }
           prometheus :9153
           forward . /etc/resolv.conf
           cache 30
           loop
           reload
           loadbalance
       }

# 在“prometheus :9153”上方添加hosts相关信息，配置IP地址和域名。
   hosts {
               192.168.1.2 domain

               fallthrough
           }
# 配置完成后，重启coredns
$ kubectl rollout restart deployment -n kube-system coredns 
```

**操作步骤**

{{% alert title="说明" %}}
成功创建OpenStack账号后，由于云管平台获取不到OpenStack平台上存储的真正容量，所以需要在[存储-块存储](../../../storage/block)页面设置OpenStack存储容量，请尽量将存储容量设置为存储的真实容量以尽可能的使用存储，避免由于设置的容量超出存储的真实容量而导致磁盘创建失败
{{% /alert %}}

1. 在云账号页面单击列表上方 **_"新建"_** 按钮，进入新建云账号页面。
2. 选择云平台为OpenStack，单击 **_"下一步：配置云账号"_** 按钮，进入配置云账号页面。
3. 配置以下参数：
   - 名称：OpenStack账号的名称。 
   - 认证地址：OpenStack管理平台的认证地址，如[http://host:port/v3](http://host:port/v3)。
   - 账号：OpenStack平台的管理员用户名，如admin。   
   - 密码：OpenStack平台管理员用户的密码。   
   - 项目：OpenStack平台上的项目，如admin项目。  
   - Domain Name：OpenStack平台上的Domain name，如default。
   - 域：选择云账号所属的域。当云账号私有状态下，域下所有项目用户都可以使用云账号创建资源。
   - 资源归属项目：OpenStack平台只支持将云账号上的资源按照云上项目归类且默认资源归属项目不能手动指定，如需更改默认资源归属项目，请在订阅列表中更改项目。勾选自动创建项目将会在{{<oem_name>}}平台创建与云上项目同名的本地项目，并将资源同步到对应项目中。云上没有项目归属的资源将会同步到默认资源归属项目。
   - 代理：当云账号需要代理才可以正常访问时设置该项，留空代表直连。如没有合适的代理，直接单击“新建”超链接，在弹出的新建代理对话框中设置相关参数，创建代理。 
   - 自动同步：设置是否自动同步OpenStack平台上的信息，并设置自动同步的时间间隔，最低为30分钟。
   - 共享范围：设置云账号的共享范围，默认为不共享，则仅云账号所在域可以使用该账号，若设置为全局共享，则平台上所有用户都可以使用该云账号创建资源。
4. 单击 **_"连接测试"_** 按钮，测试输入的参数是否正确。
5. 测试成功后，单击 **_"下一步：定时同步任务设置（可选）"_** 按钮，进入定时同步任务设置页面配置云账号的同步任务使得云账号自动同步行为更加可控。定时同步任务设置页面选填，如不需要在{{<oem_name>}}平台设置自动同步任务，可直接单击 **_"跳过"_** 按钮。如需要在{{<oem_name>}}平台中设置云账号自动同步的时间，请配置相关参数，配置完成且测试成功后，单击 **_"确定"_** 按钮，创建OpenStack账号。

### 新建ZStack/DStack账号

**支持版本**

支持纳管ZStack 3.5.0版本及之后版本。

**操作步骤**

1. 在云账号页面单击列表上方 **_"新建"_** 按钮，进入新建云账号页面。
2. 选择云平台为ZStack或DStack，单击 **_"下一步：配置云账号"_** 按钮，进入配置云账号页面。
3. 配置以下参数：
   
   - 名称：ZStack或DStack账号的名称。  
   - 认证地址：ZStack或DStack平台的认证地址，一般为[http://host:8080/](http://host:8080/)，host为ZStack或DStack控制节点的IP地址。 
   - 密钥ID：即ZStack或DStack平台上的Access Key ID。 
   - 密码：即ZStack或DStack平台上的Access Key Secret。
{{% alert title="说明" %}}
用户可在ZStack管理平台的[平台管理-Access Key]页面中生成新的Access Key信息或使用已有的Access Key。
{{% /alert %}}
   - 域：选择云账号所属的域。当云账号私有状态下，域下所有项目用户都可以使用云账号创建资源。
   - 资源归属项目：选择将云账号上的资源同步到{{<oem_name>}}平台的本地项目。如需将云账号上的资源按照云上项目归类，请先指定默认资源归属项目，并勾选自动创建项目。勾选后，将会在{{<oem_name>}}平台创建与云上项目同名的本地项目，并将资源同步到对应项目中。云上没有项目归属的资源将会同步到默认资源归属项目。
   - 代理：当云账号需要代理才可以正常访问时设置该项，留空代表直连。如没有合适的代理，直接单击“新建”超链接，在弹出的新建代理对话框中设置相关参数，创建代理。
   - 自动同步：设置是否自动同步ZStack/DStack平台上的信息，并设置自动同步的时间间隔。
   - 共享范围：设置云账号的共享范围，默认为不共享，则仅云账号所在域可以使用该账号，若设置为全局共享，则平台上所有用户都可以使用该云账号创建资源。
4. 单击 **_"连接测试"_** 按钮，测试输入的参数是否正确。
5. 测试成功后，单击 **_"下一步：定时同步任务设置（可选）"_** 按钮，进入定时同步任务设置页面配置云账号的同步任务使得云账号自动同步行为更加可控。定时同步任务设置页面选填，如不需要在{{<oem_name>}}平台设置自动同步任务，可直接单击 **_"跳过"_** 按钮。如需要在{{<oem_name>}}平台中设置云账号自动同步的时间，请配置相关参数，配置完成且测试成功后，单击 **_"确定"_** 按钮，创建ZStack/DStack账号。

### 新建阿里飞天云

该功能用于纳管阿里飞天私有云，目前仅支持同步飞天私有云上的资源。

**支持版本**

支持纳管飞天 v3.12.0及之后版本。

**操作步骤**

1. 在云账号页面单击列表上方 **_"新建"_** 按钮，进入新建云账号页面。
2. 选择云平台为飞天，单击 **_"下一步：配置云账号"_** 按钮，进入配置云账号页面。
3. 配置以下信息：
    - 名称：飞天云账号的名称。
    - 密钥ID/密码：通过Access Key验证方式对接阿里云平台，Access Key由密钥ID（Access Key ID）和密码（Access Key Secret）组成。具体请参考[飞天云相关参数获取方式](#飞天云相关参数获取方式)
    - 秘钥ID: 假设秘钥是: NbzBaQ94MPzjZf5i, 可查看的最高组织Id是: 4, 则秘钥需要填写: NbzBaQ94MPzjZf5i/4
    - 域：选择云账号所属的域。当云账号私有状态下，域下所有项目用户都可以使用云账号创建资源。
   - 资源归属项目：选择将云账号上的资源同步到{{<oem_name>}}平台的本地项目。
   - 代理：当云账号需要代理才可以正常访问时设置该项，留空代表直连。如没有合适的代理，直接单击“新建”超链接，在弹出的新建代理对话框中设置相关参数，创建代理。
   - 自动同步：设置是否自动同步阿里飞天平台上的信息，并设置自动同步的时间间隔。
   - 共享范围：设置云账号的共享范围，默认为不共享，则仅云账号所在域可以使用该账号，若设置为全局共享，则平台上所有用户都可以使用该云账号创建资源。
4. 单击 **_"连接测试"_** 按钮，测试输入的参数是否正确。
5. 测试成功后，单击 **_"下一步：定时同步任务设置（可选）"_** 按钮，进入定时同步任务设置页面配置云账号的同步任务使得云账号自动同步行为更加可控。定时同步任务设置页面选填，如不需要在{{<oem_name>}}平台设置自动同步任务，可直接单击 **_"跳过"_** 按钮。如需要在{{<oem_name>}}平台中设置云账号自动同步的时间，请配置相关参数，配置完成且测试成功后，单击 **_"确定"_** 按钮，创建阿里飞天私有云账号。

#### 飞天云相关参数获取方式

##### 飞天云获取Accesskey

只有运营管理员和一级组织管理员可以获取组织AccessKey。

1. 管理员登录ASCM控制台。
2. 在页面顶部菜单栏上，单击 **_"企业"_** 。
3. 在 **_"企业"_** 页面的左侧导航栏中，单击 **_"组织管理"_** 。
4. 在组织结构中，单击要添加的上级组织后面的设置图标。
5. 在弹出的下拉菜单中，选择 **_"获取AccessKey"_** 。
6. 在弹出的对话框中，查看组织Accesskey信息。
7. 组织Id获取需要打开浏览器调试，查找ListResourceGroup API请求, 在返回值里面找第一个organizationID

##### 飞天云获取Endpoint

1. 在地址栏中，输入ASO的访问地址region-id.aso.intranet-domain-id.com，按回车键。
2. 输入正确的用户名及密码，单击 **_"登录"_** ，进入ASO页面。
3. 在页面左侧导航栏中，单击 **_"产品运维管理 > 产品列表 > 天基"_** ，跳转到天基控制台页面。
4. 在天基控制台左侧导航栏中选择 **_"报表"_** 。
5. 在 **_"全部报表"_** 页面搜索 **_"服务注册变量"_** 。单击 **_"服务注册变量"_** 。
6. 在服务注册变量页面，单击Service旁边的图标，搜索对应产品服务。
7. 在服务的Service Registration列中，单击鼠标右键，选择 **_"选择更多"_** 。
8. 在 **_"详情"_** 页面查看产品服务的Endpoint地址。

### 新建HCSO账号

该功能用于纳管HCSO账号。

1. 在云账号页面单击列表上方 **_"新建"_** 按钮，进入新建云账号页面。
2. 选择云平台为HCSO，单击 **_"下一步：配置云账号"_** 按钮，进入配置云账号页面。
3. 配置以下参数：
    - 名称：HCSO账号的名称。
    - 密钥ID/密码：通过Access Key验证方式对接HCSO平台，Access Key由密钥ID（Access Key ID）和密码（Access Key Secret）组成。具体请参考[HCSO相关参数获取方式](#hcso相关参数获取方式)
    - 默认区域/端点(Endpoint))域名：以地址iam.cn-north-1.test.com为例. 其中`iam`指统一身份认证服务,`cn-north-1`指端点区域,`test.com`即端点(Endpoint)域名。
    - 统一认证服务端点/弹性云服务器端点/虚拟私有云端点/镜像服务端点/云硬盘端点/分布式缓存端点/弹性负载均衡端点/对象存储服务端点/关系型数据库端点/NAT网关端点/云审计服务端点/监控服务端点/企业项目端点/文件系统（SFS Turbo）端点：选填，通过API使用资源时，需要指定对应的终端节点，请向企业管理员获取终端节点信息。
    - 子网DNS：设置环境中的子网默认DNS地址，最多可以设置两个，请使用英文','隔开.例如： 10.125.0.26,10.125.0.27。
    - 域：选择云账号所属的域。当云账号私有状态下，域下所有项目用户都可以使用云账号创建资源。
    - 资源归属项目：选择将云账号上的资源同步到{{<oem_name>}}平台的本地项目。
    - 代理：当云账号需要代理才可以正常访问时设置该项，留空代表直连。如没有合适的代理，直接单击“新建”超链接，在弹出的新建代理对话框中设置相关参数，创建代理。
    - 自动同步：设置是否自动同步HCSO平台上的信息，并设置自动同步的时间间隔。
    - 共享范围：设置云账号的共享范围，默认为不共享，则仅云账号所在域可以使用该账号，若设置为全局共享，则平台上所有用户都可以使用该云账号创建资源。
4. 单击 **_"连接测试"_** 按钮，测试输入的参数是否正确。
5. 测试成功后，单击 **_"下一步：定时同步任务设置（可选）"_** 按钮，进入定时同步任务设置页面配置云账号的同步任务使得云账号自动同步行为更加可控。定时同步任务设置页面选填，如不需要在{{<oem_name>}}平台设置自动同步任务，可直接单击 **_"跳过"_** 按钮。如需要在{{<oem_name>}}平台中设置云账号自动同步的时间，请配置相关参数，配置完成且测试成功后，单击 **_"确定"_** 按钮，创建HCSO账号。

#### HCSO相关参数获取方式

##### HCSO获取AccessKey

1. 登录HCSO控制台，鼠标悬停在右上角用户名处，选择下拉菜单 **_"我的凭证"_** 菜单项，进入我的凭证页面。

    ![](../../../images/multiplecloud/hcsoaksk.png)
2. 单击左侧[访问密钥]菜单，在访问密钥页面单击 **_"新增访问密钥"_** 按钮。

    ![](../../../images/multiplecloud/hcsoaddaksk.png)

3. 通过验证后，会下载credentials名称的Excel表格，打开表格后即可获取密钥ID（Access Key ID）和密码（Secret Access Key）。
    ![](../../../../faq/image/faq_account_huawei_3.png)

### 新建HCS账号

该功能用于纳管HCS账号。

1. 在云账号页面单击列表上方 **_"新建"_** 按钮，进入新建云账号页面。
2. 选择云平台为HCS，单击 **_"下一步：配置云账号"_** 按钮，进入配置云账号页面。
3. 配置以下参数：
    - 名称：HCS云账号的名称。
    - 备注：HCS云账号的备注。
    - 密钥ID/密码：通过Access Key验证方式对接HCS平台，Access Key由密钥ID（Access Key ID）和密码（Access Key Secret）组成。具体请参考[HCS相关参数获取方式](#hcs相关参数获取方式)。
    - 认证地址：。
    - 资源归属项目：选择将云账号上的资源同步到{{<oem_name>}}平台的本地项目。
    - 代理：当云账号需要代理才可以正常访问时设置该项，留空代表直连。如没有合适的代理，直接单击“新建”超链接，在弹出的新建代理对话框中设置相关参数，创建代理。
    - 只读模式：开启后，该云账号只会进行同步资源操作，无法进行其他任务操作，如新建、删除或修改等。
4. 单击 **_"连接测试"_** 按钮，测试输入的参数是否正确。
5. 测试成功后，单击 **_"下一步：定时同步任务设置（可选）"_** 按钮，进入定时同步任务设置页面配置云账号的同步任务使得云账号自动同步行为更加可控。定时同步任务设置页面选填，如不需要在{{<oem_name>}}平台设置自动同步任务，可直接单击 **_"跳过"_** 按钮。如需要在{{<oem_name>}}平台中设置云账号自动同步的时间，请配置相关参数，配置完成且测试成功后，单击 **_"确定"_** 按钮，创建HCS账号。

#### HCS相关参数获取方式

##### HCS获取AccessKey

1. 登录HCS控制台，鼠标悬停在右上角用户处，选择下拉菜单 **_"个人设置"_** 菜单项，进入个人设置页面。

    ![](../../../images/multiplecloud/hcsaksk.png)
2. 单击基本信息下方 **_"管理访问密钥"_** 菜单，在管理访问密钥页面单击 **_"新增访问密钥"_** 按钮。

    ![](../../../images/multiplecloud/hcsaddaksk.png)

3. 单击 **_"新增访问密钥"_** 按钮后，生成的访问密钥文件会下载到本地（csv文件），打开后即可获取密钥ID（Access Key ID）和密码（Secret Access Key）。
    ![](../../../images/multiplecloud/hcsbelongaksk.png)

### 新建Cloudpods云账号

该功能用于纳管Cloudpods账号。

1. 在云账号页面单击列表上方 **_"新建"_** 按钮，进入新建云账号页面。
2. 选择云平台为Cloudpods，单击 **_"下一步：配置云账号"_** 按钮，进入配置云账号页面。
3. 配置以下参数：
    - 名称：Cloudpods云账号的名称。
    - 认证地址：即对应的keystone服务地址，可在Cloudpods控制节点通过`ocadm cluster rcadmin`命令获取OS_AUTH_URL。一般为http://域名(IP地址):30500/v3。
    - 密钥ID/密码：通过Access Key验证方式对接Cloudpods，获取方式请参考[Cloudpods相关参数获取方式](#cloudpods相关参数获取方式)
    - 域：选择云账号所属的域。当云账号私有状态下，域下所有项目用户都可以使用云账号创建资源。
    - 资源归属项目：选择将云账号上的资源同步到{{<oem_name>}}平台的本地项目。
    - 代理：当云账号需要代理才可以正常访问时设置该项，留空代表直连。如没有合适的代理，直接单击“新建”超链接，在弹出的新建代理对话框中设置相关参数，创建代理。
    - 自动同步：设置是否自动同步HCSO平台上的信息，并设置自动同步的时间间隔。
    - 共享范围：设置云账号的共享范围，默认为不共享，则仅云账号所在域可以使用该账号，若设置为全局共享，则平台上所有用户都可以使用该云账号创建资源。
4. 单击 **_"连接测试"_** 按钮，测试输入的参数是否正确。
5. 测试成功后，单击 **_"下一步：定时同步任务设置（可选）"_** 按钮，进入定时同步任务设置页面配置云账号的同步任务使得云账号自动同步行为更加可控。定时同步任务设置页面选填，如不需要在{{<oem_name>}}平台设置自动同步任务，可直接单击 **_"跳过"_** 按钮。如需要在{{<oem_name>}}平台中设置云账号自动同步的时间，请配置相关参数，配置完成且测试成功后，单击 **_"确定"_** 按钮，创建Cloudpods账号。
#### Cloudpods相关参数获取方式

##### Cloudpods获取Accesskey

1. 登录Cloudpods平台，鼠标悬停在右上角用户名处，选择下拉菜单 **_"访问凭证"_** 菜单项，进入访问凭证页面。

    ![](../../../images/multiplecloud/cloudpodsaksk.png)

2. 在AccessKey管理页面中单击 **_"新建"_** 按钮，新建Accesskey。

    ![](../../../images/multiplecloud/cloudpodsaddaksk.png)

3. 已有AccessKey，则对应的ID、Client Secret即对应的密钥ID和密码信息。

    ![](../../../images/multiplecloud/cloudpodsaksklist.png)

### 新建Nutanix账号

该功能用于纳管Nutanix平台资源，支持纳管Nutanix V2版本。

1. 在云账号页面单击列表上方 **_"新建"_** 按钮，进入新建云账号页面。
2. 选择云平台为Cloudpods，单击 **_"下一步：配置云账号"_** 按钮，进入配置云账号页面。
3. 配置以下参数：
    - 名称：Nutanix云账号的名称。
    - 备注：Nutanix云账号的备注。
    - Prism地址：Nutanix平台的Prism web控制台的地址。
    - 端口：Prism web控制台的访问端口，默认为9440。
    - 账号、密码：即登录Prism web控制台的账号和密码。
    - 域：选择云账号所属的域。当云账号私有状态下，域下所有项目用户都可以使用云账号创建资源。
    - 资源归属项目：选择将云账号上的资源同步到{{<oem_name>}}平台的本地项目。
    - 代理：当云账号需要代理才可以正常访问时设置该项，留空代表直连。如没有合适的代理，直接单击“新建”超链接，在弹出的新建代理对话框中设置相关参数，创建代理。
    - 自动同步：设置是否自动同步HCSO平台上的信息，并设置自动同步的时间间隔。
    - 共享范围：设置云账号的共享范围，默认为不共享，则仅云账号所在域可以使用该账号，若设置为全局共享，则平台上所有用户都可以使用该云账号创建资源。
4. 单击 **_"连接测试"_** 按钮，测试输入的参数是否正确。
5. 测试成功后，单击 **_"下一步：定时同步任务设置（可选）"_** 按钮，进入定时同步任务设置页面配置云账号的同步任务使得云账号自动同步行为更加可控。定时同步任务设置页面选填，如不需要在{{<oem_name>}}平台设置自动同步任务，可直接单击 **_"跳过"_** 按钮。如需要在{{<oem_name>}}平台中设置云账号自动同步的时间，请配置相关参数，配置完成且测试成功后，单击 **_"确定"_** 按钮，创建Nutanix平台的账号。


### 新建S3账号

S3即Simple Storage service。在创建S3账号之前需要先部署基于S3协议的对象存储服务器，如MinIO等，MinIO的安装部署[参考链接](https://min.io/download#/linux)。

1. 在云账号页面单击列表上方 **_"新建"_** 按钮，进入新建云账号页面。
2. 选择云平台为S3，单击 **_"下一步：配置云账号"_** 按钮，进入配置云账号页面。
3. 配置以下参数：
    - 名称：S3对象存储服务器的名称。
    - 接入地址：S3对象存储服务器的接入地址。若部署MinIO服务器，接入地址格式为[http://IP地址:9000](http://IP地址:9000)。
    - 密钥ID：即Access Key。
    - 密码：即Secret Key。
     
    ```bash
    #在MinIO存储服务器上执行以下命令，即可获取到接入地址(Endpoint)、密钥ID(Access Key)、密码（Secret Key）信息#
    $ ./minio server /mnt/data
    Endpoint:  http://10.127.10.201:9000  http://127.0.0.1:9000
    AccessKey: XRSN7GL67M70AM342UGV
    SecretKey: mUd+e+h0DS3oIDEvF27b2EE4l+WN5MuZ2ZI+VOag
    ```
     
    - 域：选择云账号所属的域。当云账号私有状态下，域下所有项目用户都可以使用云账号创建资源。
    - 资源归属项目：选择将云账号上的资源同步到{{<oem_name>}}平台的本地项目。如需将云账号上的资源按照云上项目归类，请先指定默认资源归属项目，并勾选自动创建项目。勾选后，将会在{{<oem_name>}}平台创建与云上项目同名的本地项目，并将资源同步到对应项目中。云上没有项目归属的资源将会同步到默认资源归属项目。
    - 代理：当云账号需要代理才可以正常访问时设置该项，留空代表直连。如没有合适的代理，直接单击“新建”超链接，在弹出的新建代理对话框中设置相关参数，创建代理。
    - 自动同步：设置是否自动同步S3对象存储服务器上的信息，并设置自动同步的时间间隔。
    - 共享范围：设置云账号的共享范围，默认为不共享，则仅云账号所在域可以使用该账号，若设置为全局共享，则平台上所有用户都可以使用该云账号创建资源。
4. 单击 **_"连接测试"_** 按钮，测试输入的参数是否正确。
5. 测试成功后，单击 **_"下一步：定时同步任务设置（可选）"_** 按钮，进入定时同步任务设置页面配置云账号的同步任务使得云账号自动同步行为更加可控。定时同步任务设置页面选填，如不需要在{{<oem_name>}}平台设置自动同步任务，可直接单击 **_"跳过"_** 按钮。如需要在{{<oem_name>}}平台中设置云账号自动同步的时间，请配置相关参数，配置完成且测试成功后，单击 **_"确定"_** 按钮，创建S3账号。
   
### 新建Ceph账号

该功能用于对接并导入ceph对象存储资源。

1. 在云账号页面单击列表上方 **_"新建"_** 按钮，进入新建云账号页面。
2. 选择云平台为Ceph，单击 **_"下一步：配置云账号"_** 按钮，进入配置云账号页面。
3. 配置以下参数：
   - 名称：ceph对象存储服务器的名称。
   - 接入地址：ceph对象存储服务器的接入地址。
   - 密钥ID：ceph对象存储服务器的密钥ID。
   - 密码：密钥ID对应的密码信息。
   - 域：选择云账号所属的域。当云账号私有状态下，域下所有项目用户都可以使用云账号创建资源。
   - 资源归属项目：选择将云账号上的资源同步到{{<oem_name>}}平台的本地项目。如需将云账号上的资源按照云上项目归类，请先指定默认资源归属项目，并勾选自动创建项目。勾选后，将会在{{<oem_name>}}平台创建与云上项目同名的本地项目，并将资源同步到对应项目中。云上没有项目归属的资源将会同步到默认资源归属项目。
   - 代理：当云账号需要代理才可以正常访问时设置该项，留空代表直连。如没有合适的代理，直接单击“新建”超链接，在弹出的新建代理对话框中设置相关参数，创建代理。
   - 自动同步：设置是否自动同步Ceph对象存储上的信息，并设置自动同步的时间间隔。
   - 共享范围：设置云账号的共享范围，默认为不共享，则仅云账号所在域可以使用该账号，若设置为全局共享，则平台上所有用户都可以使用该云账号创建资源。
4. 单击 **_"连接测试"_** 按钮，测试输入的参数是否正确。
5. 测试通过后，单击 **_"确定"_** 按钮，创建Ceph账号。

### 新建XSKY账号

该功能用于对接并导入XSKY存储资源，要求用户环境中存在XSKY对象存储。

1. 在云账号页面单击列表上方 **_"新建"_** 按钮，进入新建云账号页面。
2. 选择云平台为XSKY，单击 **_"下一步：配置云账号"_** 按钮，进入配置云账号页面。
3. 配置以下参数：
   - 名称：XSKY存储服务器的名称。
   - 接入地址：XSKY存储服务器的接入地址。
   - 密钥ID：XSKY对象存储服务器的密钥ID。
   - 密码：密钥ID对应的密码信息。
   - 域：选择云账号所属的域。当云账号私有状态下，域下所有项目用户都可以使用云账号创建资源。
   - 资源归属项目：选择将云账号上的资源同步到{{<oem_name>}}平台的本地项目。如需将云账号上的资源按照云上项目归类，请先指定默认资源归属项目，并勾选自动创建项目。勾选后，将会在{{<oem_name>}}平台创建与云上项目同名的本地项目，并将资源同步到对应项目中。云上没有项目归属的资源将会同步到默认资源归属项目。
   - 代理：当云账号需要代理才可以正常访问时设置该项，留空代表直连。如没有合适的代理，直接单击“新建”超链接，在弹出的新建代理对话框中设置相关参数，创建代理。
   - 自动同步：设置是否自动同步XSKY对象存储上的信息，并设置自动同步的时间间隔。
    - 共享范围：设置云账号的共享范围，默认为不共享，则仅云账号所在域可以使用该账号，若设置为全局共享，则平台上所有用户都可以使用该云账号创建资源。
4. 单击 **_"连接测试"_** 按钮，测试输入的参数是否正确。
5. 测试成功后，单击 **_"下一步：定时同步任务设置（可选）"_** 按钮，进入定时同步任务设置页面配置云账号的同步任务使得云账号自动同步行为更加可控。定时同步任务设置页面选填，如不需要在{{<oem_name>}}平台设置自动同步任务，可直接单击 **_"跳过"_** 按钮。如需要在{{<oem_name>}}平台中设置云账号自动同步的时间，请配置相关参数，配置完成且测试成功后，单击 **_"确定"_** 按钮，创建XSKY账号。

## 全量同步

该功能用于全量同步账号上的资源信息。

{{% alert title="注意" color="warning" %}}
- 禁用状态的云账号不支持全量同步；
{{% /alert %}}

**单个云账号全量同步**

1. 在云账号页面，单击云账号右侧操作列 **_"全量同步"_** 按钮，全量同步云账号上的资源信息。

**批量全量同步**

1. 在云账号列表勾选一个或多个云账号，单击列表上方 **_"批量操作"_** 按钮，选择下拉菜单 **_"全量同步"_** 菜单项，全量同步云账号上的资源信息。

## 设置自动同步

该功能用于设置云账号是否开启自动同步，并设置自动同步间隔时间。自动同步即增量同步云账号上的资源。

**云账号设置自动同步**

1. 在云账号页面，单击云账号右侧操作列 **_"更多"_** 按钮，选择下拉菜单 **_"设置自动同步"_** 菜单项，弹出设置定时任务对话框。
2. 单击**_"新建"_** 按钮，进入配置自动同步页面。
3. 配置以下参数：
   - 名称：定时任务的名称。
   - 触发频率：支持单次、每天、每周、每月的自定义时间。
   - 触发时间：选择具体的时间作为触发时间，例如：2000-01-01 00:00。

## 更新账号密码

该功能用于更新云账号的账号和密码信息。不同平台的云账号参数不同。不同平台账号密码获取方式请参考对应的新建云账号章节。禁用状态的云账号不支持该操作。

{{% alert title="注意" color="warning" %}}
VMware云账号暂不支持更新账号。
{{% /alert %}}

1. 在云账号列表中，分别单击不同平台云账号操作列 **_"更多"_** 按钮，选择下拉菜单 **_"更新账号密码"_** 菜单项，弹出更新账号密码对话框。
2. 修改不同平台的账号密码信息，修改完成后，单击 **_"确定"_** 按钮。

## 更新账单文件

该功能用于更新云账号的账单文件，仅阿里云、华为云、AWS、Azure、Google支持。不同平台的账单文件参数不同，不同平台账号密码获取方式请参考对应的新建云账号章节。

1. 在云账号列表中，分别单击不同平台云账号操作列 **_"更多"_** 按钮，选择下拉菜单 **_"更新账单文件"_** 菜单项，进入更新账单文件页面。
2. 修改不同平台的账单文件参数，修改完成后，单击 **_"确定"_** 按钮。

## 连接测试

该功能用于测试账号的连接状态并同步云账号上的资源信息。禁用状态的云账号不支持该操作。

**单个云账号连接测试**

1. 在云账号页面，单击云账号右侧操作列 **_"更多"_** 按钮，选择下拉菜单 **_"连接测试"_** 菜单项，测试账号连接状态，若处于云账号连接状态则同步云账号上资源信息。

**批量连接测试**

1. 在云账号列表勾选一个或多个云账号，单击列表上方 **_"批量操作"_** 按钮，选择下拉菜单 **_"连接测试"_** 菜单项，测试账号连接状态，若处于云账号连接状态则同步云账号上资源信息。

## 设置优惠率

该功能用于为公有云账号设置优惠率。设置优惠率后，用户创建公有云资源时显示的估算价格为优惠后的价格。

{{% alert title="说明" %}}
- 对公有云云账号设置优惠率，不会影响公有云上的实际账单费用。
- 仅在云账号共享范围内创建资源才会显示优惠后的价格。
{{% /alert %}}

1. 在云账号页面，单击云账号右侧操作列 **_"更多"_** 按钮，选择下拉菜单 **_"设置优惠率"_** 菜单项，弹出设置优惠率对话框。
2. 设置优惠率（优惠后价格=原价*（1-优惠率）），单击 **_"确定"_** 按钮，完成操作。

## 设置共享

该功能用于设置云账号的共享状态。

云账号不同与其它域资源，有5种共享情况。

- 不共享（私有）：即云账号上的资源仅云账号所属域可用。
- 共享云订阅-部分（多域共享云订阅）：当共享云订阅，并指定部分域后，管理员可以在订阅页面更改项目，只能选择订阅共享的域下的项目。设置完成后，云账号资源只有项目所在域中的用户使用。
- 共享云订阅-全部（全局共享云订阅）：当共享云订阅选择全部域后，管理员以在订阅页面更改项目，可以选择任意域下的项目。设置完成后，云账号资源只有项目所在域中的用户使用。
- 共享云账号-部分（多域共享云账号）：即云账号可以共享到指定域（一个或多个），只有云账号所在域和共享域下的用户可以使用云账号。
- 共享云账号-全部（全局共享云账号）：即云账号可以共享给全部域使用，即系统中所有用户都可以使用云账号。


{{% alert title="说明" %}}
设置共享的条件：需同时满足

- 当前用户在管理后台。
- 在{{<oem_name>}}已开启三级权限。
{{% /alert %}}

{{% alert title="注意" color="warning" %}}
通过云账号同步下来的资源（除安全组外）的共享范围都受云账号的共享范围影响。云账号上的资源其他域是否可用需要看资源的具体共享范围。
{{% /alert %}}

1. 在云账号页面，单击云账号右侧操作列 **_"更多"_** 按钮，选择下拉菜单 **_"设置共享"_** 菜单项，弹出设置共享对话框。
2. 配置以下参数：
   - 当共享范围选择为“不共享”时，即云账号的共享范围为私有，仅云账号所属域可以使用云账号的资源。
   - 当共享范围选择为“共享云订阅”时，需要选择共享的域。
       - 当域选择其中一个或多个域时，即云账号的共享范围为共享云订阅-部分，后续订阅更改项目时的选择范围为共享域下的任意项目。更改项目后，仅项目所属域可以使用云账号的资源。
       - 当域选择全部时，即云账号的共享范围为共享云订阅-全部，后续订阅更改项目时的可选范围为任意域下的任意项目。更改项目后，仅项目所属域可以使用云账号的资源。
   - 当共享范围选择为“共享云账号”是，需要选择共享的域。
       - 当域选择其中一个或多个域时，即云账号的共享范围为共享云账号-部分，只有云账号所在域和共享域下的用户可以使用云账号的资源。
       - 当域选择全部时，即云账号的共享范围为共享云账号-全部，系统中的所有用户都可以使用云账号资源。
3. 单击 **_"确定"_** 按钮，完成操作。

## 设置代理

该功能用于帮助已创建好的云账号绑定代理。

1. 在云账号页面，单击云账号右侧操作列 **_"更多"_** 按钮，选择下拉菜单 **_"设置代理"_** 菜单项，弹出设置代理对话框。
2. 选择代理，单击 **_"确定"_** 按钮。

## 开启免密登录

该功能用于开启云账号的免密登录功能，将系统的SAML信息同步到云账号上，并成为云上登录的身份提供商。开启后,在云账号详情-免密登录页面添加的免密用户可以免密登录公有云平台。目前暂不支持关闭该功能。

{{% alert title="说明" %}}
目前支持免密登录的公有云平台：阿里云、腾讯云、华为云、AWS。
{{% /alert %}}

1. 在云账号页面，单击云账号右侧操作列 **_"更多"_** 按钮，选择下拉菜单 **_"开启免密登录"_** 菜单项，弹出操作确认对话框。
2. 单击 **_"确定"_** 按钮，完成操作。

## 启用

该功能用于启用"禁用"状态的云账号，禁用状态的云账号的资源不能被使用。

**单个启用**

1. 在云账号页面，单击"禁用"状态的云账号右侧操作列 **_"更多"_** 按钮，选择下拉菜单 **_"启用"_** 菜单项，弹出操作确认对话框。
2. 单击 **_"确定"_** 按钮，启用云账号。

**批量启用**

1. 在云账号列表中勾选一个或多个"禁用"状态的云账号，单击列表上方 **_"批量操作"_** 按钮，选择下拉菜单 **_"启用"_** 菜单项，弹出操作确认对话框。
2. 单击 **_"确定"_** 按钮，启用云账号。


## 禁用

该功能用于禁用"启用"状态的云账号。删除之前需要先禁用云账号。

**单个禁用**

1. 在云账号页面，单击"启用"状态的云账号右侧操作列 **_"更多"_** 按钮，选择下拉菜单 **_"禁用"_** 菜单项，弹出操作确认对话框。
2. 单击 **_"确定"_** 按钮，禁用云账号。

**批量禁用**

1. 在云账号列表中勾选一个或多个"启用"状态的云账号，单击列表上方 **_"批量操作"_** 按钮，选择下拉菜单 **_"禁用"_** 菜单项，弹出操作确认对话框。
2. 单击 **_"确定"_** 按钮，禁用云账号。

## 删除

该功能用于删除云账号。删除之前需要先禁用云账号。在{{<oem_name>}}平台上删除云账号不会影响到云账号上的资源。

**单个删除**

1. 在云账号页面，单击"禁用"状态的云账号右侧操作列 **_"更多"_** 按钮，选择下拉菜单 **_"删除"_** 菜单项，弹出操作确认对话框。
2. 单击 **_"确定"_** 按钮，完成操作。

**批量删除**

1. 在云账号列表中勾选一个或多个"禁用"状态的云账号，单击列表上方 **_"批量操作"_** 按钮，选择下拉菜单 **_"删除"_** 菜单项，弹出操作确认对话框。
2. 单击 **_"确定"_** 按钮，完成操作。

## 查看云账号详情

该功能用于查看云账号的详细信息。

1. 在云账号页面，单击指定云账号名称项，进入云账号详情页面。
2. 详情页面顶部菜单项支持对云账号进行更新账号密码、全量同步、设置自动同步、连接测试、设置为共享、设置为私有、启用、禁用、删除等操作。
3. 查看以下信息：
   - 基本信息：包括云上ID、ID、名称、状态、域、项目、共享范围、平台、账号、代理、启用状态、同步时间、创建时间、更新时间、备注等。
   - 账号信息：包括环境、健康状态、余额、虚拟机数量、宿主机数量。

## 查看宿主机信息

该功能用于查看私有云平台以及VMware平台的宿主机信息。公有云账号无该页面。

1. 在云账号页面，单击“宿主机”页签，进入宿主机页面。
2. 查看宿主机信息，并支持对宿主机进行管理操作。

## 查看资源统计信息

该功能用于统计云账号下的资源信息。

1. 在云账号详情页面，单击“资源统计”页签，进入资源统计页面。
2. 查看以下信息：
    - 查看虚拟机数量、LB实例数量、RDS实例数量、Redis实例数量、存储桶的数量、对象存储容量、EIP的数量、公网IP的数量、快照的数量、VPC的数量、IP子网的数量、IP总量。
    - 查看虚拟机关机率：关机状态的虚拟机占虚拟机总数量的百分比。包括关机状态的虚拟机数量、未关机状态的虚拟机数量（包括异常、开机等状态）、虚拟机总数量；
    - 磁盘挂载率：挂载到虚拟机的磁盘数量占磁盘总数量的百分比。包括已挂载到虚拟机的磁盘数量、未挂载到虚拟机的磁盘数量、磁盘总数量；
    - EIP使用率：EIP挂载到虚拟机的数量占EIP总数量的百分比。包括EIP已使用的数量、未使用的数量、EIP总数量；
    - IP使用率：IP被使用的数量占IP总数量的百分比；包括IP已使用的数量、未使用的数量、IP总数量。

## 订阅管理

订阅类似于子账号。通过云账号和订阅确定公有云上的可用资源。云管平台实际通过订阅在对应的公有云平台上购买资源。
订阅和云账号一样都是域资源，订阅同步下来的资源归属与云账号相同的项目，表示项目所在域下的用户都有权限使用订阅创建资源。

- VMware、OpenStack、ZStack、DStack、AWS、阿里云、腾讯云平台的云账号下只有一个订阅。
- Azure、华为云、UCloud平台的云账号下支持多个订阅，其中华为云一个订阅属于一个区域。

### 新建订阅

目前仅Azure国际区的云账号支持新建订阅。

1. 在云账号详情页面，单击“订阅”页签，进入订阅页面。
2. 单击列表上方 **_"新建"_** 按钮，弹出新建订阅对话框。
3. 配置以下信息：
    - EA账号：需要指定创建云订阅的EA账号。
    - 订阅名称：设置订阅的名称。
    - 用途：设置订阅的用途，包括开发/测试和生产。
4. 单击 **_"确定"_** 按钮，完成操作。

### 更改项目

该功能用于更改订阅所属项目，实质为更改订阅的所属域。当云账号设置共享云订阅并指定共享范围后，管理员可通过更改项目功能修改订阅所属域，可选域为云订阅的共享范围，修改完成后仅订阅所属域中的用户有权限使用订阅资源。

**单个订阅更改项目**

1. 在云账号详情页面，单击“订阅”页签，进入订阅页面。
2. 单击订阅右侧操作列 **_"更改项目"_** 按钮，弹出更改项目对话框。
3. 单击 **_"确定"_** 按钮，完成操作。

**批量更改项目**

1. 在云账号详情页面，单击“订阅”页签，进入订阅页面。
2. 在列表勾选一个或多个订阅，单击列表上方 **_"更改项目"_** 按钮，弹出更改项目对话框。
3. 单击 **_"确定"_** 按钮，完成操作。

### 全量同步

该功能用于全量同步订阅信息。

{{% alert title="说明" %}}
- 当云账号只有一个订阅，全量同步订阅等同于全量同步云账号。
- 当云账号有多个订阅，如华为云，全量同步订阅仅同步订阅下的区域信息。
{{% /alert %}}

1. 在云账号详情页面，单击“订阅”页签，进入订阅页面。
2. 单击订阅右侧操作列 **_"全量同步"_** 按钮，同步订阅信息。

### 启用订阅

当订阅处于”启用“状态，且状态处于“已连接”时，用户可以正常使用订阅在对应的公有云平台的区域中创建资源。

**单个启用**

1. 在云账号详情页面，单击“订阅”页签，进入订阅页面。
2. 单击"禁用"状态的订阅右侧操作列 **_"更多"_** 按钮，选择下拉菜单 **_"启用"_** 菜单项，弹出操作确认对话框。
3. 单击 **_"确定"_** 按钮，完成操作。

**批量启用**

1. 在云账号详情页面，单击“订阅”页签，进入订阅页面。
2. 在列表中选择一个或多个"禁用"状态的订阅，单击列表上方 **_"启用"_** 按钮，弹出操作确认对话框。
3. 单击 **_"确定"_** 按钮，完成操作。

### 禁用订阅

当订阅处于"禁用"状态，用户无法使用订阅在对应的公有云平台的区域中创建资源。

**单个禁用**

1. 在云账号详情页面，单击“订阅”页签，进入订阅页面。
2. 单击"启用"状态的订阅右侧操作列 **_"更多"_** 按钮，选择下拉菜单 **_"禁用"_** 弹出操作确认对话框。
3. 单击 **_"确定"_** 按钮，完成操作。

**批量禁用**

1. 在云账号详情页面，单击“订阅”页签，进入订阅页面。
2. 在列表中选择一个或多个"启用"状态的订阅，单击列表上方 **_"禁用"_** 按钮，弹出操作确认对话框。
3. 单击 **_"确定"_** 按钮，完成操作。

### 删除订阅

目前仅Azure国际区的云账号支持删除订阅的功能，目前删除订阅不会影响云上，若云上还存在该订阅，下次同步时仍会出现订阅。

1. 在云账号详情页面，单击“订阅”页签，进入订阅页面。
2. 单击订阅右侧操作列 **_"更多"_** 按钮，选择下拉菜单 **_"删除"_** 弹出操作确认对话框。
3. 单击 **_"确定"_** 按钮，完成操作。

### 查看订阅详情页面

1. 在云账号详情页面，单击“订阅”页签，进入订阅页面。
2. 单击订阅名称项，进入订阅详情页面。
3. 查看以下信息。
   - 基本信息：包括云上ID、ID、名称、状态、域、项目、平台、账号、启用状态、同步时间、创建时间、更新时间、备注。
   - 其他信息：包括健康状态等。

### 查看订阅下的区域

该功能用于查看订阅下的区域信息，不同平台下的订阅支持的区域不同，其中除华为云外的公有云平台，一个订阅下支持多个区域，华为云一个订阅支持一个区域，用户在公有云平台创建虚拟机时需要根据地理位置选择对应平台可用区等。

#### 设置同步

用户可根据使用情况设置是否同步该区域的资源，例如用户不使用阿里云国外区域的资源，可通过批量设置同步功能关闭阿里云国外区域的同步功能，后续用户全量同步云账号或订阅时，将不会同步阿里云国外区域的资源，节省全量同步的时间。

**单个区域设置同步**

1. 在订阅详情页面，单击“区域”页签，进入区域页面。
2. 单击区域右侧操作列 **_"设置同步"_** 按钮，弹出设置同步对话框。
3. 选择是否同步该区域的资源，单击 **_"确定"_** 按钮。

**批量设置同步**

1. 在订阅详情页面，单击“区域”页签，进入区域页面。
2. 在列表中勾选一个或多个区域，单击列表上方 **_"设置同步"_** 按钮，弹出设置同步对话框。
3. 选择是否同步该区域的资源，单击 **_"确定"_** 按钮。 

#### 全量同步

该功能用于全量同步订阅下指定区域的资源。

1. 在订阅详情页面，单击“区域”页签，进入区域页面。
2. 单击区域右侧操作列 **_"全量同步"_** 按钮，全量同步该区域的资源。

### 查看订阅的云上配额

该功能用于查看公有云平台上的配额信息。

1. 在订阅详情页面，单击“云上配额”页签，进入云上配额页面。
2. 查看不同资源的配额使用情况。

### 查看订阅下的资源统计信息

该功能用于统计订阅下的资源信息，云账号下有多个订阅时，所有订阅的资源统计相加等于云账号下的资源统计。

1. 在订阅详情页面，单击“资源统计”页签，进入资源统计页面。
2. 查看以下信息：
    - 查看虚拟机数量、LB实例数量、RDS实例数量、Redis实例数量、存储桶的数量、对象存储容量、EIP的数量、公网IP的数量、快照的数量、VPC的数量、IP子网的数量、IP总量。
    - 查看虚拟机关机率：关机状态的虚拟机占虚拟机总数量的百分比。包括关机状态的虚拟机数量、未关机状态的虚拟机数量（包括异常、开机等状态）、虚拟机总数量；
    - 磁盘挂载率：挂载到虚拟机的磁盘数量占磁盘总数量的百分比。包括已挂载到虚拟机的磁盘数量、未挂载到虚拟机的磁盘数量、磁盘总数量；
    - EIP使用率：EIP挂载到虚拟机的数量占EIP总数量的百分比。包括EIP已使用的数量、未使用的数量、EIP总数量；
    - IP使用率：IP被使用的数量占IP总数量的百分比；包括IP已使用的数量、未使用的数量、IP总数量。


## 免密登录用户管理

该功能用于管理可以免密登录公有云以及HCSO平台的系统内用户。

### 新建免密登录用户

该功能用于将系统内的本地用户设置为公有云平台的免密登录用户。

1. 在云账号页面，单击公有云平台云账号名称项，进入云账号详情页面。
2. 单击“免密登录用户”页签，进入免密登录用户页面。
3. 单击 **_"新建"_** 按钮，弹出新建免密登录用户。
4. 关联本地用户，并选择对应云用户组。
5. 单击<确定>按钮，完成操作。

### 删除免密登录用户

该功能用于删除免密登录用户，删除后，系统内用户将无法再免密登录到公有云。

#### 删除免密登录用户

1. 在云账号页面，单击公有云平台云账号名称项，进入云账号详情页面。
2. 单击“免密登录用户”页签，进入免密登录用户页面。
3. 单击用户右侧操作列 **_"删除"_** 按钮，弹出操作确认对话框。
4. 单击 **_"确定"_** 按钮，完成操作。

#### 批量删除免密登录用户

1. 在云账号页面，单击公有云平台云账号名称项，进入云账号详情页面。
2. 单击“免密登录用户”页签，进入免密登录用户页面。
3. 在列表中选择一个或多个用户，单击 **_"删除"_** 按钮，弹出操作确认对话框。
4. 单击 **_"确定"_** 按钮，完成操作。

## 云用户管理

云用户即公有云平台（不支持天翼云和UCloud）上的用户，该功能用于管理公有云云账号下的云用户信息。

**云用户来源**

- 当云管平台对接公有云平台云账号时，将会同步公有云平台上子账号和协作者到云管平台。
- 新建云用户。

{{% alert title="说明" %}}
- 系统管理员可以在任意域的云账号管理云用户。
- 域管理员只能在本域下的云账号管理云用户。
{{% /alert %}}

### 新建云用户

该功能用于新建云用户，即在对应公有云平台上新建用户，并支持将该用户关联{{<oem_name>}}平台的本地用户。关联本地用户后，本地用户可以在用户信息处的多云统一登录查看关联的云用户信息，并支持便捷的使用云用户登录公有云平台。

1. 在云账号页面，单击公有云平台云账号名称项，进入云账号详情页面。
2. 单击“云用户”页签，进入云用户页面。
3. 单击列表上方 **_"新建"_** 按钮，弹性新建云用户对话框。
4. 配置以下参数：
   - 云订阅：仅谷歌云需要设置该参数，谷歌云的订阅对应谷歌云的项目。指定云订阅即为指定的谷歌云账号添加对应项目。
   - 用户名：设置云用户的名称，将会使用该名称在对应公有云平台（除谷歌云外）创建用户。谷歌云必须填入已存在的账号。
{{% alert title="说明" %}}
对于谷歌云来说，新建云用户操作即将谷歌云的已有账号与平台对接的谷歌云账号通过项目关联起来。
{{% /alert %}}
   - 云用户组：将云用户加入云用户组，云用户将拥有该云用户组的所有权限。
   - 关联本地用户：选择已加入项目的本地用户。
{{% alert title="说明" %}}
**管理后台**

- 当云账号共享范围是私有或共享云订阅时，仅可以选择加入云账号所在域下项目的用户。
- 当云账号共享范围是全局共享时，可以选择加入加入任意域下的项目的用户。

**域管理后台**

- 无论云账号共享范围如何，仅可以选择加入本域下项目的用户。
{{% /alert %}}
   - 邮箱：配置接收创建云用户信息的邮箱。当勾选“发送创建云用户邮件时”，将会发送创建信息到该邮箱。
{{% alert title="说明" %}}
请确保已经在通知渠道中配置了邮箱服务。
{{% /alert %}}
5. 单击 **_"确定"_** 按钮，完成操作。

### 同步状态

该功能用于获取云用户的当前状态。

1. 在云账号页面，单击公有云平台云账号名称项，进入云账号详情页面。
2. 单击“云用户”页签，进入云用户页面。
3. 单击云用户右侧操作列 **_"同步状态"_** 按钮，同步云用户状态。

### 修改本地用户

该功能用于修改云用户关联的本地用户。修改本地用户操作将会重置云用户的密码。

{{% alert title="注意" color="warning" %}}
谷歌云平台的云用户关联本地用户时不会重置密码。
{{% /alert %}}

1. 在云账号页面，单击公有云平台云账号名称项，进入云账号详情页面。
2. 单击“云用户”页签，进入云用户页面。
3. 单击云用户右侧操作列 **_"更多"_** 按钮，选择下拉菜单 **_"修改本地用户"_** 菜单项，弹出修改本地用户对话框。
4. 选择本地用户，单击 **_"确定"_** 按钮。

{{% alert title="说明" %}}
**管理后台**

- 当云账号共享范围是私有或共享云订阅时，仅可以选择加入云账号所在域下项目的用户。
- 当云账号共享范围是全局共享时，可以选择加入加入任意域下的项目的用户。

**域管理后台**

- 无论云账号共享范围如何，仅可以选择加入本域下项目的用户。
{{% /alert %}}

### 关联云用户组

该功能用于将云用户加入云用户组。云用户将拥有该云用户组的所有权限。

1. 在云账号页面，单击公有云平台云账号名称项，进入云账号详情页面。
2. 单击“云用户”页签，进入云用户页面。
3. 单击云用户右侧操作列 **_"更多"_** 按钮，选择下拉菜单 **_"关联云用户组"_** 菜单项，弹出关联云用户组对话框。
4. 选择云用户组，单击 **_"确定"_** 按钮，完成操作。

### 删除

该功能用于删除云用户，删除操作将会在对应公有云平台上删除对应用户。

**单个删除**

1. 在云账号页面，单击公有云平台云账号名称项，进入云账号详情页面。
2. 单击“云用户”页签，进入云用户页面。
3. 单击云用户右侧操作列 **_"更多"_** 按钮，选择下拉菜单 **_"删除"_** 菜单项，弹出操作确认对话框。
4. 单击 **_"确定"_** 按钮，完成操作。

**批量删除**

1. 在云账号页面，单击公有云平台云账号名称项，进入云账号详情页面。
2. 单击“云用户”页签，进入云用户页面。
3. 在列表中选择一个或多个云用户，单击列表上方 **_"批量操作"_** 按钮，选择下拉菜单 **_"删除"_** 菜单项，弹出操作确认对话框。
4. 单击 **_"确定"_** 按钮，完成操作。

### 查看云用户详情

该功能用于查看云用户详细信息。

1. 在云账号页面，单击公有云平台云账号名称项，进入云账号详情页面。
2. 单击“云用户”页签，进入云用户页面。
3. 单击云用户名称项，进入云用户详情页面。
4. 查看以下信息：包括云上ID、ID、名称、状态、域、项目、平台、登录地址、关联本地用户、控制台登录、创建时间、更新时间、备注。

### 查看云用户关联的云用户组

该功能用于查看云用户关联的云用户组，支持将云用户从云用户组移除操作。

#### 移除云用户组

该功能用于将云用户从云用户组移除。

**单个移除**

1. 在云账号页面，单击公有云平台云账号名称项，进入云账号详情页面。
2. 单击“云用户”页签，进入云用户页面。
3. 单击云用户名称项，进入云用户详情页面。
4. 单击“云用户组”页签，进入云用户组页面。
5. 单击云用户组右侧操作列 **_"删除"_** 按钮，弹出操作确认对话框。
6. 单击 **_"确定"_** 按钮，完成操作。
   
**批量移除**

1. 在云账号页面，单击公有云平台云账号名称项，进入云账号详情页面。
2. 单击“云用户”页签，进入云用户页面。
3. 单击云用户名称项，进入云用户详情页面。
4. 单击“云用户组”页签，进入云用户组页面。
5. 在列表中选择一个或多个云用户组，单击列表上方 **_"删除"_** 按钮，弹出操作确认对话框。
6. 单击 **_"确定"_** 按钮，完成操作。

### 查看云用户的操作日志

该功能用于查看云用户相关操作的操作日志。

1. 在云账号页面，单击公有云平台云账号名称项，进入云账号详情页面。
2. 单击“云用户”页签，进入云用户页面。
3. 单击云用户名称项，进入云用户详情页面。
4. 单击“操作日志”页签，进入操作日志页面。
    - 加载更多日志：列表默认显示20条操作日志信息，如需查看更多操作日志，请单击 **_"加载更多"_** 按钮，获取更多日志信息。
    - 查看日志详情：单击操作日志右侧操作列 **_"查看"_** 按钮，查看日志的详情信息。支持复制详情内容。
    - 查看指定时间段的日志：如需查看某个时间段的操作日志，在列表右上方的开始日期和结束日期中设置具体的日期，查询指定时间段的日志信息。
    - 导出日志：目前仅支持导出本页显示的日志。单击右上角![](../../../images/system/download.png)图标，在弹出的导出数据对话框中，设置导出数据列，单击 **_"确定"_** 按钮，导出日志。

## 云用户组管理

该功能用于查看云账号对应的公有云平台中可用的云用户组。如当前云用户组不满足需求，可新建云用户组。

1. 在云账号页面，单击公有云平台云账号名称项，进入云账号详情页面。
2. 单击“云用户组”页签，进入云用户组页面。
3. 对云用户组支持进行管理操作，详细请参考[云用户组](../cloudgroup/)内容。

## 查看云上项目

该功能用于查看云平台上的项目与本地项目的映射。其中VMware、OpenStack、阿里云、华为云、腾讯云、Azure平台上的项目与本地项目支持双向同步。

{{% alert title="说明" %}}
- 在云上项目的对应项目中创建资源，将会同步到对应的云上项目；
- 在没有对应云上项目的项目中创建资源，如果云平台上有同名项目，将会同步到同名项目上；若没有同名项目，则会在云上创建同名项目，并将资源同步到同名项目中。
{{% /alert %}}

### 切换本地项目

该功能用于更改本地项目与云上项目的映射关系。切换本地项目后，云账号的资源也将同步至新项目。

{{% alert title="说明" %}}
- 如云账号的资源在{{<oem_name>}}平台上已更改项目，切换本地项目将不会影响已更改项目的资源。
- 切换本地项目后，计费也将同步到新项目。
- 域的可选范围与云帐号的共享范围有关；云账号私有时，只能选择云账号所属域；云账号共享云订阅时，只能选择云订阅所属域，云账号多域共享时，可以选择云帐号所属域和共享域。
{{% /alert %}}

**切换本地项目**

1. 在云账号详情页面，单击“云上项目”页签，进入云上项目页面。
2. 单击项目对应操作列 **_"切换本地项目"_** 按钮，弹出切换本地对话框。
3. 选择域和项目，单击 **_"确定"_** 按钮。

**批量切换本地项目**

1. 在云账号详情页面，单击“云上项目”页签，进入云上项目页面。
2. 在列表中选择一个或多个项目，单击列表上方 **_"切换本地项目"_** 按钮，弹出切换本地对话框。
3. 选择域和项目，单击 **_"确定"_** 按钮。

## 查看操作日志

该功能用于查看云账号相关操作的日志信息

1. 在云账号页面，单击指定云账号名称项，进入云账号详情页面。
2. 单击“操作日志”页签，进入操作日志页面。
    - 加载更多日志：列表默认显示20条操作日志信息，如需查看更多操作日志，请单击 **_"加载更多"_** 按钮，获取更多日志信息。
    - 查看日志详情：单击操作日志右侧操作列 **_"查看"_** 按钮，查看日志的详情信息。支持复制详情内容。
    - 查看指定时间段的日志：如需查看某个时间段的操作日志，在列表右上方的开始日期和结束日期中设置具体的日期，查询指定时间段的日志信息。
    - 导出日志：目前仅支持导出本页显示的日志。单击右上角![](../../../images/system/download.png)图标，在弹出的导出数据对话框中，设置导出数据列，单击 **_"确定"_** 按钮，导出日志。

## 如何通过本系统免密登录公有云平台？

公有云平台支持基于SAML协议的单点登录功能，通过身份提供商功能，可以实现企业用户通过自己的账号体系单点登录公有云平台，并管理公有云平台的资源。

### 身份提供商

身份提供商（Identity Provider，简称IdP）用于提供身份验证，外部用户通过已知的身份提供商身份验证后，将使用角色登录公有云平台。外部用户将在角色的有限权限范围内进行资源访问。因外部身份用户登录腾讯云所用的是角色，而角色使用的是临时密钥，您可避免因长期使用密钥（例如云 API 密钥），导致难以轮换密钥以及被截取后泄露导致的安全问题。 

### 配置Azure External Identies

{{% alert title="说明" %}}
将{{<oem_name>}}平台设置为域名访问，并在全局设置-控制台地址中设置访问域名。非域名访问的平台否则无法作为Azure的External Identies。
{{% /alert %}}

1. 在{{<oem_name>}}平台获取Azure账号的ID。
    
    ![](../../../images/multiplecloud/azureaccountid.png)

2. 在浏览器中输入“https://<域名>/api/saml/idp/metadata/<账号ID>”，将显示的XML文件内容保存。例如：“[https://saml.test.cn/api/saml/idp/metadata/7c6c10d5-953a-444c-8685-d0b8f53984b2](#配置azure-external-identies)”，并保存该文件。

    ![](../../../images/multiplecloud/azurexml.png)

3. 在[Azure](https://portal.azure.com/)控制台，搜索“external identies”并进入该页面。

    ![](../../../images/multiplecloud/externalidenties.png)

4. 单击左侧菜单项“All identity providers”，进入“All identity providers”页面.

    ![](../../../images/multiplecloud/createexternalidenties.png)
    
5. 单击“New SAML/WS-Fed Idp”，在弹出的对话框中配置以下参数。
    - Identity provider protocol：选择SAML。
    - Domain name of federating IdP：设置为平台的域名，例如saml.test.cn。
    - Select a method for populating metadata：建议选择“Parse metadata file”，并上传上面步骤保存的xml文件，并单击“Parse”，自动填充下面参数。如选择“Input metadata manually”，需要安装上面的截图对应项，分别填入，注意，直接复制的Certificate项有空格，需要将空格完全删除。

    ![](../../../images/multiplecloud/newsaml.png)

6. 除此之外，还需要为Azure的应用程序添加用户权限，Azure应用程序具体可参考[获取Azure的租户ID和Client信息](#获取azure的租户-tenant-id和client信息)。
7. 在应用程序详情页面，单击“API permission”，进入API permission页面，确保应用程序有Microsoft Graph下的“User.Invite.ALL”和“User.ReadWrite.All”的权限，若没有该权限，需要单击“add a permission”，添加对应权限。

    ![](../../../images/multiplecloud/permission.png)
    ![](../../../images/multiplecloud/addpermission.png)
    ![](../../../images/multiplecloud/adduserpermission.png)

### 设置Chrome浏览器

当在{{<oem_name>}}平台免密登录Azure平台时，在登录Azure过程中需要携带Cookie回调{{<oem_name>}}平台，Chrome浏览器默认不允许跨网站携带Cookie，所以需要进行以下配置：

1. 在Chrome浏览器地址栏输入“chrome://flags/”，并搜索“SameSite by default cookies”。
2. 禁用“SameSite by default cookies”和“Cookies without SameSite must be secure”。
    ![](../../../../quickuse/images/quickstart/disablesamesite.png)

3. 重启浏览器使配置生效。

### 使用流程

1. 在{{<oem_name>}}平台上创建云账号时，开启免密登录功能，此时将会把系统的SAML信息上传到公有云平台，使系统作为公有云平台的身份提供商。
2. 在云用户组页面，创建对应平台云用户组，并选择对应权限。
3. 在云账号详情-免密登录用户页面，新建免密登录用户，关联本地用户并指定用户所属的云用户组。该操作用于授予系统内用户免密登录公有云的权限。
4. 后续关联云上SAML用户的本地用户，可在 **_"用户信息-多云统一登录-免密登录用户"_** 中单击 **_"免密登录"_** 按钮，将会以指定的权限免密登录公有云平台。

{{% alert title="注意" color="warning" %}}
在{{<oem_name>}}平台免密登录Azure平台时，仍需要输入用户的账号。目前登录账号未在前端展示，格式为：用户名@域名。例如saml.test.cn环境上的test用户免密访问Azure平台，用户账号为test@saml.test.cn。
{{% /alert %}}
