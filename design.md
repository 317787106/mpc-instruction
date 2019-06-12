# Tron第一阶段powersoftau初步流程设计
* 发布匿名交易的项目背景和需求，号召社区用户参与；并在github的wiki上记录时间节点和对应的操作流程；
* 在社区选取m个参与者，规划每个用户的参与时间节点，每个参与者预留4小时的参与时间（1小时下载/环境准备+1小时计算+1小时上传+1小时冗余），
* 组织者：生成第一个challenge文件（5分钟），并发布到aliyun云存储（1小时）；
* 组织者：发邮件或通过keybase通知第 i 个用户challenge文件的下载地址；
* 参与者(4小时)：   
  1.rust运行环境准备及下载challenge文件，1.2GB（1小时）；   
  2.执行compute流程，中间需要用户随机至少32字节的随机字符串（1小时）；   
  3.完成后把hash值、response文件、硬件信息等通过keybase客户端发送给组织者（1小时）； 
  4.销毁机器，避免信息泄露；
* 组织者（5小时）：   
  1.验证response文件（4小时）；
  2.若验证成功，生成new_challenge文件和response_hash值；把new_challenge上传到aliyun云存储（1小时），把new_challenge文件链接和hash发布到github的wiki。这个new_challenge是后一个参与者的challenge文件。每个参与者一个目录。
  3.若验证失败，丢弃此次response文件；
  4.通知第i+1个参与者，转4。
* 组织者：在所有m个用户参与完成后   
  1.添加随机信标，生成response文件。   
  2.把最终的response文件上传到aliyun云存储，把beacon值发布到github的wiki。
* 所有人：验证最终的response，生成22个参数文件；
* 组织者：把这22个文件发布到amazon云存储服务器。

# Tron第二阶段mpc初步流程设计

* 发布项目背景和需求，号召社区用户参与；并在github的wiki上记录时间节点和对应的操作流程；

* 在社区选取n个参与者，规划用户的参与时间节点，每个参与者预留8个小时的参与时间（1小时下载+1小时环境准备+4小时计算+1小时上传+1小时冗余），1天大约可以让2个参与者完成；

* 把zcash第一阶段发布的22个参数文件（2.3GB）发布到amazon云存储服务器；

* 组织者：生成第一个param文件（770MB），发布到aliyun云存储服务器；

* 组织者：发邮件或通过keybase通知第 i 个用户params文件的下载地址；

* 参与者（4小时）：   
  rust运行环境准备（1小时）；
  下载22个参数文件和params文件（1小时）；
  执行compute流程（4小时）；
  完成后把hash值、new_params文件、硬件信息等通过keybase客户端发送给组织者（1小时）；

* 组织者：   
  验证new_params是否可信：
  若验证失败，丢弃本次new_params文件；  
  若验证成功，把new_params上传到aliyun云存储，并把参与者的名称、hash值、时间记录和new_params链接发布到github的wiki。每个用户一个目录   
  通知第i+1个参与者；

* 组织者：
  在所有n个用户参与完成后添加随机信标beacon；   
  把params文件上传到amazon，把hash和params文件链接发布到github的wiki；

* 所有用户分割params文件，可以得到output，spend的proof key、verify key文件；
