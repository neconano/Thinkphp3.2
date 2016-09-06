# Thinkphp3.2

### 版本特性

开发快，效率和tp一样

1.需要使用自定义模式 MyCore ，可参考入口代码

```php
define('APP_MODE','MyCore');
define ( 'APP_PATH', SYS_PATH_R.'Application/' );
/**
 * 缓存目录设置
 * 此目录必须可写，建议移动到非WEB目录
 */
define ( 'RUNTIME_PATH', SYS_PATH_R.'Runtime/' );
/**
 * 引入核心入口
 * ThinkPHP亦可移动到WEB以外的目录
 */
require CORE_PATH_R.'ThinkPHP/ThinkPHP.php';
```

2.主要自定义函数mycreate和myRcreate

可根据传入数据（是否有主键）自动判断新增或修改，并默认使用create方法

```php
$input = I('post.');
$id = D2("StyOutlineCourseware")->mycreate($input);
```

3.模型自动完成定制

```php
array('modify_user', 'fix_user', 2,'callback','modify_user',1),//array('field','填充内容','填充条件','附加规则',[额外参数],[表单数据标记])
```
