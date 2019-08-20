# RDS定时备份

本脚本自动创建一个lambda以及相关资源，使得能够自动对指定RDS每隔两小时备份一次。

您可以通过点击下方 **Quick Start** 链接直接进入创建页面。

[Quick Start](https://console.amazonaws.cn/cloudformation/home?region=cn-north-1#/stacks/new?stackName=backup-rds&templateURL=s3://quickstart-rds-backup/rds-backup.yaml) 

## 前提条件

需要在目标区域拥有RDS。

## 实现步骤

- 在您的AWS账户中启动AWS CloudFormation 模板。

![](https://raw.githubusercontent.com/fanyizhe/rds-backup/master/CFN.png)

- 检查导航栏右上角显示的所在区域，根据需要进行更改。

- 在 **指定模板** 页面上，保留模板 URL 的默认设置，然后选择 **下一步** 。
![](https://raw.githubusercontent.com/fanyizhe/rds-backup/master/CFN_template.png)

- 在 **指定堆栈详细信息** 页面上，填写堆栈名称、您想应用该脚本的RDS实例名称,以及您想保存最大的副本数量(最大100)，完成后选择 **下一步**

    - rdsInstanceName: 您想应用该脚本的RDS实例名称
    - MaxSnapshotNumber: 您想保存最大的副本数量(最大100)

![](https://raw.githubusercontent.com/fanyizhe/rds-backup/master/specifyInfo.png)

- （可选）在 **配置堆栈选项** 页面上，您可以为堆栈中的资源 [指定标签](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-resource-tags.html) (键/值对) 并 [设置高级选项](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-console-add-tags.html)。在完成此操作后，选择 **下一步** 。

- 在 **审核** 页面上，查看并确认模板设置。选择 **功能** 下的复选框，以确认模板将创建 IAM 资源。

![](https://raw.githubusercontent.com/fanyizhe/rds-backup/master/capability.png)

-  选择 **创建堆栈** 以部署堆栈。
- 监控堆栈的状态。当状态为 **CREATE\_COMPLETE** 时，表示脚本及资源创建已完成。

![](https://raw.githubusercontent.com/fanyizhe/rds-backup/master/create_complete.png)

## （可选）自定义修改备份时间

该脚本默认自动创建备份的时间为2小时。

若您希望对自动备份的时间进行自定义修改的话，具体操作如下：

- 在该cloudformation的 **资源** 选项中点击类型为 **AWS::Lambda::Function** 的实体ID链接，进入该lambda函数界面。

![](https://raw.githubusercontent.com/fanyizhe/rds-backup/master/CFN_lambda.png)

- 在 **Designer** 界面中点击 **CloudWatch Events** 图标， 在下方出现的触发事件界面中点击该规则链接，进入 **事件规则** 页面。

![](https://raw.githubusercontent.com/fanyizhe/rds-backup/master/cloudWatch_event.png)

- 在该事件规则界面中，选择右上角 **操作** 按钮，点击进入 **编辑** 页面。

![](https://raw.githubusercontent.com/fanyizhe/rds-backup/master/edit_event.png)

- 在 **事件源** 界面中，您可以修改触发事件的固定频率，或者使用 [规则的计划表达式](https://docs.amazonaws.cn/AmazonCloudWatch/latest/events/ScheduledEvents.html)，完成后点击 **配置详细信息** 进入下一页面，然后点击 **保存修改** 。

![](https://raw.githubusercontent.com/fanyizhe/rds-backup/master/edit_event2.png)
