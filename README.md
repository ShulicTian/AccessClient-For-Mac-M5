# AccessClient-For-Mac-M5
齐治科技 AccessClient Mac M5 闪退问题修复

## 日志最后显示在执行命令文件
/usr/bin/open /var/folders/hn/f0p0cpvd4j3_7b7385p9ppl80000gp/T/tmp4fc2vrfh.command

## 命令窗口显示结果
> connecting ...
> add 'HostkeyAlgorithms +ssh-rsa' to ~/.ssh/config
>
> Saving session...  
> ...copying shared history...  
> ...saving history...truncating history files...  
> ...completed.  
>
> [进程已完成]

## 解决方案
1. 访达进入 /Application/AccessClient 的显示包内容
<img width="570" height="352" alt="image" src="https://github.com/user-attachments/assets/094bc504-04bc-47e6-af3b-754b7548348f" />

2. 进入Contents/Resources/Scripts/Loader
<img width="1840" height="872" alt="image" src="https://github.com/user-attachments/assets/0fef0d80-d68a-4819-8fef-23619a80bd32" />


3. 编辑template_file.py 加上-o HostkeyAlgorithms=+ssh-rsa参数
<img width="2716" height="552" alt="image" src="https://github.com/user-attachments/assets/5406b96b-0b5f-4d3a-b716-3453d0bcaad9" />

> set pid [spawn ssh $user\@$host -p $port -o PreferredAuthentications=password -o PubkeyAuthentication=no -o StrictHostKeyChecking=no -o HostkeyAlgorithms=+ssh-rsa]

## 闪退原因
部分堡垒机使用旧的算法,例如 ssh-dss, Mac M5 自带的 ssh 版本较高,已完全淘汰或默认不使用一些旧算法,使用参数指定添加对就算法的支持即可连接成功
