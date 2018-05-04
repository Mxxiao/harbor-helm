# Helm Chart for Harbor

## Introduction

derive: [https://github.com/vmware/harbor/tree/master/contrib/helm/harbor](https://github.com/vmware/harbor/tree/master/contrib/helm/harbor)



安装harbor 
这里官方提供了两种方式，Insecure和Secure，我这里选用的是Secure安全的部署方式，让harbor自己生成CA和SSL，简单方便。执行如下命令安装harbor: 

helm install . --debug --name hub --set externalDomain=harbor.my.domain 

externalDomain为外部能访问到harbor的域名，到目前为止，你可以在本地/etc/hosts中添加域名解析，从本地访问进行测试，待测试完成后再加入traefik-ingress中，当然你也可以直接在traefik-ingress中添加域名解析。