## 使用docker安装

- 执行docker命令如下：

  ``` bash
  Step 1:
  Run: docker network create mynet
  
  Step 2:
  Run: docker run --name sonar-postgres -e POSTGRES_USER=sonar -e POSTGRES_PASSWORD=sonar -d -p 5432:5432 --net mynet postgres
  
  Step 3:
  Run: docker run --name sonarqube -p 9000:9000 -e SONARQUBE_JDBC_USERNAME=sonar -e SONARQUBE_JDBC_PASSWORD=sonar -e SONARQUBE_JDBC_URL=jdbc:postgresql://sonar-postgres:5432/sonar -d --net mynet sonarqube:5.6
  ```

## 数据

- sonarcloud Android项目的token： **c011dd6b125d7f3e913028de38c24bb1c874d9a2**



## 可能碰到的坑

- sonarqube的要求运行内存至少是2G，所以如果你内存低于2G就不要白费功夫了。

