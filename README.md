# 中国大陆 省 - 市 - 区县 - 社区 四级数据
数据来源：http://www.stats.gov.cn/tjsj/tjbz/tjyqhdmhcxhfdm/2016/index.html

在网上找到很多的省市区县的数据中四个直辖市（北京、上海、天津、重庆）的数据都是如下这样

> 北京市 - 北京市 - 东城区

这样的数据，二级数据，和一级数据一样，在感官上给用户造成多余的感觉。
感觉这样不好。就自己弄一个格式。
把这4个直辖市的 三级数据提升为二级数据，如下这样

> 北京市 - 东城区 - 东华门

使用户选择的时候也顺畅一点。



## 数据目录说明

```
|- all-lv3.txt  省 - 市 - 区县 三级完整的 json 数据包
|
|- all-lv4.txt  省 - 市 - 区县 - 社区 四级完整的 json 数据包 
|
|- mysql-city-lv3.sql  mysql 数据库三级数据导入sql
|
|- mysql-city-lv4.sql  mysql 数据库四级数据导入sql
|
|- vue-city-lv3.json  element（饿了么开源的vue组件库）组件库中 el-cascader 级联组件和 iview 组件库中的 Cascader  可以直接使用的json数据 
|
|- vue-city-lv4.json  同 vue-city-lv3.json 四级json数据
|
|- list-lv4     省 - 事 - 区县 - 单个省、直辖市四级数据包
|- - - 北京市.json
|- - - ...
|
|- list-lv5     省 - 事 - 区县 - 单个省五级数据包，其中四个直辖市数据只有4级数据，没有第五级数据
|- - - 北京市.json
|- - - ...
```

## 数据格式
```
{
    name:'北京',list:[
        {name:'东城区'，list:[
            {name:'东华门',list:[
                {name:'多福巷'},{name:'银闸'},{...}
            ]}
        ]}
    ] 
}
```

## 数据库 表设计
```
CREATE TABLE `china_city` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `name` varchar(255) DEFAULT NULL,
  `level` int(11) DEFAULT NULL,
  `parent_id` bigint(20) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8mb4; 
```





如果有其他格式需要，可以解析 json 数据包，然后自行拼装所需要的格式


## 重要说明
+ 北京 、天津 、上海、重庆 四个直辖市 的 二级数据为 区，三级数据为 街道，四级数据为 社区。
+ 省中的 直辖县 数据合并为二级数据。
