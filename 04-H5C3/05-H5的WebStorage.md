# 本地存储

> 1、本地存储：localStorage、sessionStorage。
>
> 2、面试经常问：localStorage、sessionStorage的用法、区别
>
> 3、本地存储和cookie、session是不同的，它存在什么地方？
>
> 浏览器右击检查-》Application里。
>
> 4、key、value形式，跟对象差不多。通过JS进行操作。

# 区别

localStorage ==》一执行，永久性保存
sessionStorage ==》关闭浏览器自动消失

# 用法

它们的用法一样：设置、获取、删除

```
1》localStorage		
2》sessionStorage

设置:（3种写法，可不给value或为空。设置完刷新页面就有了）
	xxx.setItem(key,value)	如localStorage.SetItem('name','zhangsan');
	xxx.name1 = '李四';
	xxx['name2'] = '王五';
获取:（也3种。收藏、记住密码等都会用到它）还需要打印或其它操作
	xxx.getItem(key)
	xxx.key
	xxx['key']
删除:	
	删除某个:
		xxx.removeItem(key);
	全部删除:
		xxx.clear();
```

# 🔺注意点

本地存储的所有值都是**string类型**（字符串）

# 案例-移动app收藏效果

大概步骤

- 获取
- 判断：提示或累加 。（因为会被覆盖，需要累加）
  - 累加——要放到数组里
    - 问题：本地存储特性——给本地存储传[]，会是字符串
    - 应对：
      - 给本地存储传[]（注意：给它个判断——没有才传[]）；
      - 通过json.parse转换为数组；
      - 然后如果不重复就push内容，否则就算了；
      - 最后把数组转换为字符串再放到本地存储中。
- 读到一个位置上。
  - 遍历获取该字符串里的数组的键值对
  - 把这些键值对加到一个空数组里
  - 然后传到对应位置上