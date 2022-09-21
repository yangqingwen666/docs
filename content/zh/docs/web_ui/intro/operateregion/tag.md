---
title: "标签"
weight: 5
description: >
    介绍标签相关操作。
---

**标签说明**

- 标签是一组键值对（key-value）。
- 一个资源支持绑定20个标签。
- 一个资源上的任一标签的键必须唯一，相同键的值将会覆盖。
- ![](../../../images/intro/label1.png)：暂无标签。
- ![](../../../images/intro/labelon1.png)：已有标签。

{{% alert title="说明" %}}
- 目前支持与公有云平台双向同步标签的资源：虚拟机、LB、NAT、CDN、NAS、RDS、Redis、MongoDB、Kafka、Elasticsearch等。
- 安全组、DNS、SSL证书等配置类资源由于与公有云平台存在一对多的关系，仅支持在{{<oem_name>}}平台管理标签，不支持与公有云平台双向同步标签。
{{% /alert %}}

**绑定标签**

{{% alert title="注意" color="warning" %}}
当为资源绑定已有标签时，可选的标签都是本地计算资源分类下的标签。
{{% /alert %}}

1. 在虚拟机列表中，将鼠标悬停在虚拟机对应标签列![](../../../images/intro/label1.png)图标上，在弹出的对话框中，单击 **_"编辑标签"_** 按钮，弹出编辑标签对话框。
2. 支持新建标签或绑定已有标签。
    - 绑定已有：单击 **_"已有标签"_** 按钮，显示已有的本地标签，选择标签键和值（可选），选择完成后，将在标签虚线框中显示标签。
    - 新建标签：单击列表上方 **_新建_** 按钮，设置标签键和标签值（可选），单击 **_"添加"_** 按钮，新建的标签将在标签虚线框中显示。

    ![](../../../images/intro/edittag.png)

3. 设置完成后，单击 **_"确定"_** 按钮，为资源绑定标签。

**批量绑定标签**

1. 在虚拟机列表中勾选多个虚拟机，单击列表上方 **_"批量操作"_** 按钮，选择下拉菜单 **_"编辑标签"_** 菜单项，弹出标记标签对话框。
2. 支持新建标签或绑定已有标签。
    - 绑定已有：单击 **_"已有标签"_** 按钮，显示已有的本地标签，选择标签键和值（可选），选择完成后，将在标签虚线框中显示标签。
    - 新建标签：单击列表上方 **_新建_** 按钮，设置标签键和标签值（可选），单击 **_"添加"_** 按钮，新建的标签将在标签虚线框中显示。

在资源列表支持通过标签搜索符合条件的资源。

{{% alert title="说明" %}}
标签键和标签值都支持搜索，此外还支持以下搜索规则：

- 默认为contains搜索标签键或标签值；
- n* 表示以n开头的标签键或标签值；
- *n 表示以n结尾的标签键或标签值；
- !n 表示不包含n（英文状态！）的标签键或标签值；
{{% /alert %}}

**解绑标签**

1. 在虚拟机列表中，单击列表上方 **_"标签"_** 按钮，根据标签过滤搜索符合条件的资源。
    - 选择无标签资源，将筛选出所有不带标签的资源。
    - 选择一个或多个标签键，若不选择标签值，将筛选出所有带指定标签键的资源。当选择具体标签值时，将筛选出所有带指定标签键和值的资源。
      
      ![](../../../images/intro/tagsearch1.png) 

1. 在虚拟机列表中，将鼠标悬停在虚拟机对应标签列![](../../../images/intro/labelon1.png)图标，弹出的对话框中将显示资源绑定的标签信息，单击对话框上的 **_"编辑标签"_** 按钮，弹出编辑标签对话框。
2. 支持解绑或更改标签。
    - 解绑标签：单击标签虚线框上标签右侧"x"，删除标签，为资源解绑标签。

      ![](../../../images/intro/deltag.png)

    - 更改标签：更改标签操作包括为资源绑定标签或解绑标签等。
     
3. 单击 **_"确定"_** 按钮，更改或解绑标签。