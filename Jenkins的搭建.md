## 用docker搭建Jenkins

- 执行如下命令即可：

  ``` bash
  sudo docker run -dit --name myjenkins -p 8081:8081  -u 0 -v /home/docker/jenkins-home:/var/jenkins_home  jenkins -e JAVA_OPTS=-Duser.timezone=Asia/Shanghai
  # 解释下每个参数的含义
  # -p 映射端口，容器暴漏的端口
  # -d 指定容器运行于后台
  # -v 指定容器挂载的目录 注意冒号前是本地路径，后面是容器路径
  # -u 0 这命令的意思是覆盖容器中内置的帐号，该用外部传入，这里传入0代表的是root帐号Id，否则会有权限问题
  ```



## 用war包搭建Jenkins

- 将war包下载下来，然后执行命令：

  ``` bash
  nohup java -Xms512m -Xmx1024m -XX:PermSize=256M -XX:PermSize=1024M -jar /usr/src/jenkins.war --httpPort=8080  &
  ```

### android环境配置问题

- 安装sdk及更新对应的tools

  ``` bash
  # 下载对应的sdk
  $ curl http://dl.google.com/android/android-sdk_r24.4.1-linux.tgz -o android-sdk_r24.4.1-linux.tgz
  # 解压文件
  $ tar -xvf android-sdk_r24.4.1-linux.tgz
  # 配置环境变量（不介绍了）
  # 获取当前可更新的sdk
  $ android list sdk -u (--all是获取所有sdk)
  # 选择要升级的sdk，进行升级
  $ android update sdk -u -t 1,2,3,5,6,8,10
  ```


## 容易出现的坑

- 阿里云服务器需要添加安全组（将对应的端口号添加上）。否则无法通过外网地址：端口号来访问部署的Jenkins。

- -u 0 参数一定要加上，否则会一直报权限异常。

- 用docker搭建的Jenkins，经常会因为内存不足而退出，且环境变量配置都不太方便，最后还是决定用java命令来搭建Jenkins。

