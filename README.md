# Helm Chart for Harbor

## Introduction

derive: [https://github.com/vmware/harbor/tree/master/contrib/helm/harbor](https://github.com/vmware/harbor/tree/master/contrib/helm/harbor)



安装harbor 
这里官方提供了两种方式，Insecure和Secure，我这里选用的是Secure安全的部署方式，让harbor自己生成CA和SSL，简单方便。执行如下命令安装harbor: 
```
helm install . --debug --name hub --set externalDomain=harbor.my.com 
```
externalDomain为外部能访问到harbor的域名，到目前为止，你可以在本地/etc/hosts中添加域名解析，从本地访问进行测试，待测试完成后再加入traefik-ingress中，当然你也可以直接在traefik-ingress中添加域名解析。


NFS的安装配置（Ubuntu 16.04/k8s1.9/helm2.9）
参考： https://www.cnblogs.com/MoreExcellent/p/7222895.html

一、服务器端：

1.1安装NFS服务：

#执行以下命令安装NFS服务器，

#apt会自动安装nfs-common、rpcbind等13个软件包


```
sudo apt install nfs-kernel-server
```

 

1.2编写配置文件：

#编辑/etc/exports 文件：

```
sudo vi /etc/exports
```

 

#/etc/exports文件的内容如下：

```
/tmp *(rw,sync,no_subtree_check,no_root_squash)

/data *(rw,sync,no_subtree_check,no_root_squash)

/logs *(rw,sync,no_subtree_check,no_root_squash)
```


 

1.3创建共享目录

#在服务器端创建/tmp /data和/logs共享目录

```
sudo mkdir -p /tmp

sudo mkdir -p /data

sudo mkdir -p /logs
```

 

1.4重启nfs服务：


```
sudo service nfs-kernel-server restart
```

```
nfs command: showmount -e <nfs-serverip> #查看nfs挂载情况
```