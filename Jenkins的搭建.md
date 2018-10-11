## 用docker搭建Jenkins

- 执行如下命令即可：

  ``` bash
  sudo docker run -dit --name myjenkins -p 8081:8081  -u 0 -v /home/docker/jenkins-home:/var/jenkins_home  jenkins
  # 解释下每个参数的含义
  # -p 映射端口，容器暴漏的端口
  # -d 指定容器运行于后台
  # -v 指定容器挂载的目录 注意冒号前是本地路径，后面是容器路径
  # -u 0 这命令的意思是覆盖容器中内置的帐号，该用外部传入，这里传入0代表的是root帐号Id，否则会有权限问题
  ```

## 容易出现的坑

- 阿里云服务器需要添加安全组（将对应的端口号添加上）。否则无法通过外网地址：端口号来访问部署的Jenkins。
- -u 0 参数一定要加上，否则会一直报权限异常。