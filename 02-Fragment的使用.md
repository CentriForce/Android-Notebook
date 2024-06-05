# Fragment的使用

首先提出几个问题

- Fragment是什么,与Activity相比有什么不同
- 创建一个Fragment需要什么?
- 如何初始化Fragment

## Fragment是什么?

Fragment是Activity内部的一个模块或子视图  
每个Fragment都有自己的布局,生命周期和事件处理方法  
Activity中的Fragment可以独立地添加,移除或替换

Fragment有以下特点:

- 灵活:可以在运行时动态添加
- 适配:可以适应不同尺寸的屏幕
- 模块化:将Activity分解为Fragment模块,在每个模块中实现各自的功能
- 生命周期:Fragment有自己独立的生命周期,可以更好地管理

## 创建一个Fragment需要什么?

### 在哪里显示Fragment?

首先,与Activity相同,Fragment也需要一个`layout文件`   
不同的是,Activity的页面会占满整个屏幕  
一般一个屏幕只有一个Activity

而一个Activity中插入了许多个Fragment  
所以要在Activity的`布局文件`中**添加Fragment标签**  
来定义Fragment的插入位置

### 在哪里创建Fragment?

Fragment与Activity相同,有自己的`生命周期`  
与创建Activity相同,Fragment`需要自己的类`

Fragment在创建的时候,会调用`onCreate`方法,执行Fragment的初始化操作

然后会进入`onCreateView`方法,在这里绑定Fragment的布局文件

视图创建完成后,进入`onViewCreated`方法  
对Fragment布局文件的修改,都放在这个方法中

## 如何初始化Fragment

如果需要动态添加Fragment,需要在Activity中获取`FragmentManager`  
然后,创建一个`FragmentTransaction`对象,获取Fragment的Transaction表单  
这个表单用于提交自己要更改的Fragment信息

接下来,使用自己定义的Fragment类,创建一个对象  
使用`FragmentTransaction`**添加fragment对象**  
最后,使用`FragmentTransaction.commit()`提交更改

详细代码如下:

``` java
FragmentManager fragmentManager = getSupportFragmentManager();
FragmentTransaction fragmentTransaction = fragmentManager.beginTransaction();
MyFragment myFragment = new MyFragment();
fragmentTransaction.add(R.id.fragment_container, myFragment);
fragmentTransaction.commit();
```

其中,`fragmentManager`一般为类内属性,而`fragmentTransaction`是方法内的临时变量
`MyFragment`是你自定义的`Fragment`类
`R.id.fragment_container`是在`Activity`中划分给`MyFragment`的显示区域

**核心**就是使用FragmentManager取FragmentTransaction  
然后使用FragmentTransaction来管理Fragment的添加,替换和移除
