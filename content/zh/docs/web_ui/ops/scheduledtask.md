---
title: "定时任务"
weight: 2
description: 定时任务即在指定的时间点对关联资源进行指定动作。  
---

定时任务即在指定的时间点对关联资源进行指定动作。目前仅支持对虚拟机进行定时开关机、重启等操作。

**入口**：在云管平台单击左上角![](../../images/intro/nav.png)导航菜单，在弹出的左侧菜单栏中单击 **_"运维工具/常用工具/定时任务"_** 菜单项，进入定时任务页面。

   ![](../../images/ops/scheduledtask.png)

## 新建定时任务

该功能用于创建定时任务。

1. 在定时任务页面，单击列表上方 **_"新建"_** 按钮，进入新建定时任务也没。
2. 配置以下参数：
    - 指定项目：管理员和域管理员在新建定时任务时需要指定定时任务所属的项目。
    - 名称：设置定时任务的名称。
    - 触发频率：支持选择单次、每天、每周、每月。
        - 当选择“单次”时，设置具体的触发时间。
        - 当选择“每天”时，设置每天具体的触发时间，并设置有效时间。定时任务在有效时间内生效。
        - 当选择“每周”时，选择具体触发星期、触发时间，并设置有效时间。定时任务在有效时间内生效。
        - 当选择“每月”时，选择具体的触发日期、触发时间，并设置有效时间。定时任务在有效时间内生效。
    - 资源类型：目前仅支持虚拟机。
    - 操作动作：目前仅支持开机、关机、重启。
    - 指定虚拟机：选择执行定时任务的虚拟机。单击输入框，在弹出的对话框中选择虚拟机，选择完成后，单击 **_"选择"_** 按钮。
3. 单击 **_"确定"_** 按钮，创建定时任务。

## 关联资源

该功能用于选择执行定时任务的虚拟机。

1. 在定时任务页面，单击定时任务右侧操作列 **_"关联资源"_** 按钮，弹出关联资源对话框。
2. 单击输入框，在弹出的对话框中选择虚拟机，选择完成后，单击 **_"选择"_** 按钮。
3. 选中的虚拟机将会反显在输入框中，此时点击名称右侧的"x"将会取消选择虚拟机。
4. 单击 **_"确定"_** 按钮，完成操作。

## 启用

该功能用于启用"禁用"状态的定时任务，禁用状态的定时任务将不生效。

**单个启用**

1. 在定时任务页面，单击"禁用"状态的定时任务右侧操作列 **_"更多"_** 按钮，选择下拉菜单 **_"启用"_** 菜单项，弹出操作确认对话框。
2. 单击 **_"确定"_** 按钮，完成操作。

**批量启用**

1. 在列表中选择一个或多个"禁用"状态的定时任务，单击列表上方 **_"批量操作"_** 按钮，选择下拉菜单 **_"启用"_** 菜单项，弹出操作确认对话框。
2. 单击 **_"确定"_** 按钮，完成操作。

## 禁用

该功能用于禁用"启用"状态的定时任务，禁用状态的定时任务将不生效。

**单个禁用**

1. 在定时任务页面，单击"启用"状态的定时任务右侧操作列 **_"更多"_** 按钮，选择下拉菜单 **_"禁用"_** 菜单项，弹出操作确认对话框。
2. 单击 **_"确定"_** 按钮，完成操作。

**批量禁用**

1. 在列表中选择一个或多个"启用"状态的定时任务，单击列表上方 **_"批量操作"_** 按钮，选择下拉菜单 **_"禁用"_** 菜单项，弹出操作确认对话框。
2. 单击 **_"确定"_** 按钮，完成操作。

## 删除

该功能用于删除定时任务。

**单个删除**

1. 在定时任务页面，单击定时任务右侧操作列 **_"更多"_** 按钮，选择下拉菜单 **_"删除"_** 菜单项，弹出操作确认对话框。
2. 单击 **_"确定"_** 按钮，完成操作。

**批量删除**

1. 在列表中选择一个或多个定时任务，单击列表上方 **_"批量操作"_** 按钮，选择下拉菜单 **_"删除"_** 菜单项，弹出操作确认对话框。
2. 单击 **_"确定"_** 按钮，完成操作。

## 查看定时任务详情

该功能用于查看定时任务的详细信息。

1. 在定时任务页面，单击定时任务名称项，进入定时任务详情页面。
2. 查看基本信息：包括云上ID、ID、名称、状态、域、项目、启用状态、操作动作、资源类型、资源数量、资源绑定、策略详情、创建时间、更新时间、备注。

## 查看任务历史

该功能用于查看定时任务执行的历史记录。

1. 在定时任务详情页面，单击“任务历史”页签，进入任务历史页面。
2. 查看任务的ID、执行状态、开始时间、结束时间等。
3. 当定时任务执行失败时，可单击右侧操作列 **_"查看"_** 按钮，查看错误日志。

## 查看定时任务的关联资源

该功能用于查看定时任务关联的资源。

1. 在定时任务详情，单击“关联资源”页签，进入关联资源页面。
2. 查看关联资源的信息。

### 关联资源

该功能用于选择执行定时任务的虚拟机。

1. 在关联资源页面，单击列表上方 **_"关联资源"_** 按钮，弹出关联资源对话框。
2. 单击输入框，在弹出的对话框中选择虚拟机，选择完成后，单击 **_"选择"_** 按钮。
3. 选中的虚拟机将会反显在输入框中，此时点击名称右侧的"x"将会取消选择虚拟机。
4. 单击 **_"确定"_** 按钮，完成操作。

### 解绑资源

该功能用于解除定时任务与虚拟机的绑定。

1. 在关联资源页面，单击资源右侧操作列 **_"解绑"_** 按钮，弹出操作确认对话框。
2. 单击 **_"确定"_** 按钮，完成操作。

## 查看操作日志

1. 在定时任务详情页面，单击“操作日志”页签，进入操作日志页面。
    - 加载更多日志：列表默认显示20条操作日志信息，如需查看更多操作日志，请单击 **_"加载更多"_** 按钮，获取更多日志信息。
    - 查看日志详情：单击操作日志右侧操作列 **_"查看"_** 按钮，查看日志的详情信息。支持复制详情内容。
    - 查看指定时间段的日志：如需查看某个时间段的操作日志，在列表右上方的开始日期和结束日期中设置具体的日期，查询指定时间段的日志信息。
    - 导出日志：目前仅支持导出本页显示的日志。单击右上角![](../../../images/system/download.png)图标，在弹出的导出数据对话框中，设置导出数据列，单击 **_"确定"_** 按钮，导出日志。 