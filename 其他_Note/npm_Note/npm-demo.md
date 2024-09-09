# npm 如何删除或设置NPM代理

1、设置http代理

```bash
npm config set proxy=http://代理服务器地址:端口号
```

2、取消代理

```bash
npm config delete proxy
```

3、npm设置淘宝镜像

```bash
npm config set registry=https://registry.npm.taobao.org
```

4、npm取消淘宝镜像

```bash
npm config delete registry
```

5、查看代理信息（当前配置）

```bash
npm config list
```

![image-20240311212908153](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240311212908153.png)
