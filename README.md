# Spring Boot-Shiro-Vue
提供一套基于SpringBoot-shiro-vue的权限管理思路.

前后端都加以控制,做到按钮/接口级别的权限

为确保密码安全，增加动态加盐加密

# 设计思路

### 核心

 	每个登录用户拥有各自的N条权限,比如 文章:查看/编辑/发布/删除

### 数据库设计：
主要4张表，其中：
用户表sys_user：可以被指定角色，（注意：还可以设计为5张表，在用户和角色加中间表，多对多关系，用户可以被指定多个角色，请自行扩展）
角色表sys_role：角色表与用户表和权限表进行关联
权限表sys_permission：执行用户权限，可以做到接口级别，只有指定权限的人才能调用接口
角色权限中间表sys_role_permission:角色和权限多对多关系

### 后端：
用户添加，会动态生成盐保存到数据库，明文密码也会被盐加密后保存
用户登录，会将登录密码加盐加密后与数据库密码比对
用户授权，会查询数据库中角色，对应角色权限进行授权
