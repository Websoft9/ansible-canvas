# 故障处理

此处收集使用 Canvas 过程中最常见的故障，供您参考

> 大部分故障与云平台密切相关，如果你可以确认故障的原因是云平台造成的，请参考[云平台文档](https://support.websoft9.com/docs/faq/zh/tech-instance.html)

#### 如何查看错误日志？

通过如下两种日志检索关键词 **Failed** 或者 **error** 查看错误

* Canvas 日志：`/data/wwwroot/canvas/log/production.log`
* Apache 日志：`/data/logs/apache`

#### Canvas服务无法启动？

服务无法启动最常见的问题包括：磁盘空间不足，内存不足，配置文件错误。  
建议先通过命令进行排查  

```shell
# 查看磁盘空间
df -lh

# 查看内存使用
free -lh

# 查看服务状态和日志
systemctl status apache
journalctl -u apache
```

#### 403 访问权限错误？

需要确保 Canvas 根目录具有 canvas 和 www-data 两个用户的权限


### 文件上传，不能下载
文件上传后，下载出现“无法访问网站 找不到canvas.example.com服务器IP地址 ”
解决办法：
1. 找到apache配置文件/etc/apache2/conf.d/vhost.conf，将默认的ServerName canvas.example.com更改为 ServerName 实际部署站点域名
2. 找到域名配置文件/data/wwwroot/canvas/config/domain.yml，将 production 配置节点的 **domain** 项的值修改为你的域名
