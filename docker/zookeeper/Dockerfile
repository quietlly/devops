############################################
# version : birdben/zookeeper:v1
# desc : 当前版本安装的zookeeper
############################################
# 设置继承自我们创建的 jdk7 镜像
FROM birdben/jdk7:v1

# 下面是一些创建者的基本信息
MAINTAINER birdben (191654006@163.com)

# 设置环境变量，所有操作都是非交互式的
ENV DEBIAN_FRONTEND noninteractive

# 添加 supervisord 的配置文件，并复制配置文件到对应目录下面。（supervisord.conf文件和Dockerfile文件在同一路径）
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# 设置 zookeeper 的环境变量，若读者有其他的环境变量需要设置，也可以在这里添加。
ENV ZOOKEEPER_HOME /software/zookeeper-3.4.8
ENV PATH ${ZOOKEEPER_HOME}/bin:$PATH

# 复制 zookeeper-3.4.8 文件到镜像中（zookeeper-3.4.8 文件夹要和Dockerfile文件在同一路径）
ADD zookeeper-3.4.8 /software/zookeeper-3.4.8

# 创建myid文件存储路径
RUN mkdir -p /var/zookeeper/myid

# 授权ZOOKEEPER_HOME路径给admin用户
RUN sudo chown -R admin /software/zookeeper-3.4.8

# 容器需要开放Zookeeper 2181端口
EXPOSE 2181

# 执行supervisord来同时执行多个命令，使用 supervisord 的可执行路径启动服务。
CMD ["/usr/bin/supervisord"]