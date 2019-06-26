# zabbix-aliyun-monitor -- mysql
Aliyun RDS-mysql status monitor with zabbix   

zabbix通过阿里云api 自动发现、监控阿里云RDS-MySQL实例
此项目参考了https://github.com/XWJR-Ops/zabbix-RDS-monitor，在其基础上进行了重构

## 使用方法
### 注意事项
1. 脚本会收集Redis别名作为监控项名称前缀展示；
2. 不要默认别名和中文别名（zabbix不识别）

### 环境要求
python = 2.7+ 或 python3.6+  其他版本未测试

### 安装依赖包
```shell
# python2
/usr/bin/env pip2 -r requirements.txt
```
```shell
# python3
/usr/bin/env pip3 -r requirements.txt
```

### 使用方法
1. 从阿里云控制台获取 **AccessKey** ,并修改脚本中的 **API_Key** 与 **API_Secret**
2. 修改区域 **RegionId**
3. 将check和discovery两个脚本放置于以下目录
```shell
cp check_rds.py discovery_rds.py /etc/zabbix/script
```
4. 将aliyun-rds.conf文件放置到以下目录，并修改其中的python版本信息（默认python3）
```shell
cp aliyun-rds.conf /etc/zabbix/zabbix_agentd.d/
```

**由于有重试机制，请修改zabbix server和agent配置中的Timeout参数为10秒以上**

5. 重启zabbix-agent
6. zabbix控制台导入模板zbx_Aliyun_RDS_MySQL_templates.xml，并关联主机