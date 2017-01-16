### mongodb环境

1. 拉取镜像 `docker pull mongo:latest` 

2. 在合适位置创建了数据文件夹后

   ```Bash
   docker run -v /Users/wk/dockers/mongodb_data:/data/db -v /Users/wk/dockers/public_share:/public_share -p 27017:27017 --name localmongodb -d mongo mongod --smallfiles
   ```

### mysql环境

1. 拉取镜像

2. 运行容器

   ```Bash
   docker run --name localmysql -v /Users/wk/dockers/mysql_data:/var/lib/mysql -v /Users/wk/dockers/public_share:/public_share -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -d mysql:latest
   ```

3. 进入交互模式

   ```
   docker exec -it localmysql bash
   ```

4. 修改访问权限

   ```Bash
   mysql> grant all privileges on *.* to 'root'@'%' identified by 'password123';
   mysql> update `mysql`.`user` set `Grant_priv` = 'Y' where `user` = 'root';
   mysql> delete from user where user='root' and host='localhost';
   mysql> flush privileges;
   ```

   参考： http://blog.bccn.net/%E9%9D%99%E5%A4%9C%E6%80%9D/61795

5. 提交镜像

   ```Bash
   docker commit localmysql mysql_image
   ```

6. 重新启动

   ```Bash
   docker run --name localmysql -v /Users/wk/dockers/mysql_data:/var/lib/mysql -v /Users/wk/dockers/public_share:/public_share -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -d mysql_image:latest
   ```

   ​

