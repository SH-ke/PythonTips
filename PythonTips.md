# $ Python $ 笔记 $ PythonTips $

## 01. $ Anaconda $ 环境配置

```shell
# 环境变量
D:\Users\86180\Anaconda
D:\Users\86180\Anaconda\Scripts\
D:\Users\86180\Anaconda\Library\bin
D:\Users\86180\Anaconda\Library\mingw-w64\binD:\Users\86180\Anaconda
# 横行-环境变量
D:\Users\86180\Anaconda;D:\Users\86180\Anaconda\Scripts\;D:\Users\86180\Anaconda\Library\bin;D:\Users\86180\Anaconda\Library\mingw-w64\binD:\Users\86180\Anaconda;

# 用conda创建Python虚拟环境（在conda prompt环境下完成）
conda create -n environment_name python=X.X
# (注：该命令只适用于Windows环境；“environment_name”是要创建的环境名；“python=X.X”是选择的Python版本)
# 删除一个已有的虚拟环境
conda remove --name your_env_name --all

# 新建notebook环境
source activate myenv # 激活环境
python -m ipykernel install --user --name myenv --display-name "Python (myenv)"
# 查看当前 kernel
jupyter kernelspec list
# 删除kernel
jupyter kernelspec remove kernelname
```

### 1.1  $ pip\; freeze $ 导出含有路径 $ (@ file:///) $ 问题小记

当你遇到此类问题时，可以暂时考虑使用如下命令生成 `requirements.txt` 文件

```shell
pip freeze > requirements.txt
# 导出依赖
pip list --format=freeze > requirements.txt
# 安装依赖
pip install -r requirements.txt
```


使用上述命令导出的文件中，会包含如下几个包：`distribute`，`pip`，`setuptools`，`wheel`，建议手动删除！

## 02. $ pandas \;\&\; numpy \;\&\; matplotlib $

运算

```python
# 第0列为index 只读取前3列
pd.read_excel(path, index_col=0, usecols=range(3))
# 切片取一行或多行
data.iloc[0,].values
data.iloc[0:70,].values
# 转置 L
list(map(list, zip(*L)))

# DataFrame 最大、最小、求和、均值
corr["MAX"]=corr[featureNames].max(axis=1)
corr["MIN"]=corr[featureNames].min(axis=1)
corr["Mean"]=corr[featureNames].sum(axis=1)
corr["Mean"]=corr[featureNames].mean(axis=1)
# DataFrame 排序
df2.sort_values(by='b')
# ascending：布尔型，True则升序，
# 如果by=['列名1','列名2']，则该参数可以是[True, False]，即第一字段升序，第二个降序。

# DataFrame apply方法
# 求每列的最大值与最小值的差
a = df.apply(lambda x:x.max()-x.min())
# 求每行的最大值与最小值的差
b = df.apply(lambda x:x.max()-x.min(), axis=1)
```
标准绘图
```python
# 标准绘图
plt.rcParams['font.family'] = ['sans-serif']
plt.rcParams['font.sans-serif'] = ['SimHei']
plt.rcParams['axes.unicode_minus'] = False
plt.rcParams['figure.figsize'] = (8.0, 5.0)

plt.title("{}工位生产100剂{}疫苗消耗时间的概率分布函数".format(infos[0], infos[1]), y=1.03, fontsize=14.5) 
# plt.ylim((-10,150))
plt.ylabel(u'$F(x)$', fontsize=13.5)
plt.xlabel(u'生产100剂疫苗所消耗时间$t_m$/s', fontsize=13.5)
plt.xticks(rotation=360)
# plt.savefig('p1.png')
plt.show()
```

不同类型的图标

```python 
# 二维散点
N = 1000
x = np.random.randn(N)
y = np.random.randn(N)
plt.scatter(x, y)
plt.show()
```



三维标准绘图

```python
# 三维绘图 旋转抛物面
# 根据已知条件 alpha=0, beta=90
# 绘制出理想的抛物曲面
fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')
plt.rcParams['font.family'] = ['sans-serif']
plt.rcParams['font.sans-serif'] = ['SimHei']
plt.rcParams['axes.unicode_minus']=False
plt.rcParams['figure.figsize'] = (12.0, 10.0)
theta = np.linspace(0, np.pi * 2, 100)
phi = np.linspace(0, np.pi / 6, 100)

p = 1
r = 1
theta, phi = np.meshgrid(theta, phi)
x = r * np.cos(theta) * np.sin(phi)
y = r * np.sin(theta) * np.sin(phi)
z = r**2 * 1/(2*p) * np.sin(phi)**2 - 300
ax = plt.subplot(111, projection='3d')

# ax.set_zlim3d(zmin=0, zmax=100)
ax.set_xlabel('x axis') #x轴名称
ax.set_ylabel('y axis') #y轴名称
ax.set_zlabel('z axis') 
ax.plot_surface(x, y, z, rstride=1, cstride=1, cmap='rainbow')
plt.title("理想旋转抛物面", fontsize=20)
plt.savefig("1.2py理想旋转抛物面.png")
plt.show()
```

```python
# numpy 生成数组之 linspace arange
A = arange(1, 5, 2)  # 步长默认为2
x = linspace(0, 2*pi, N+1)  # N+1个点
```



## 03. 国内源

Windows 用户无法直接创建名为 `.condarc` 的文件，可先执行 `conda config --set show_channel_urls yes` 生成该文件。生成的文件在`C:\Users\用户名\.condarc`

```shell
# conda文件
# 中科大镜像源
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/conda-forge/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/msys2/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/bioconda/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/menpo/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/
# 北京外国语大学源
conda config --add channels  https://mirrors.bfsu.edu.cn/anaconda/pkgs/main
conda config --add channels  https://mirrors.bfsu.edu.cn/anaconda/pkgs/free
conda config --add channels  https://mirrors.bfsu.edu.cn/anaconda/pkgs/r
conda config --add channels  https://mirrors.bfsu.edu.cn/anaconda/pkgs/pro
conda config --add channels  https://mirrors.bfsu.edu.cn/anaconda/pkgs/msys2
#清华源
conda config --add channels  https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
conda config --add channels  https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
conda config --add channels  https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
conda config --add channels  https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/pro
conda config --add channels  https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
```

## 04.$virtualenv$ 使用

### 4.1 新建环境

```shell
# 跳转到指定目录，在该目录下新建环境 cv2 指定 python 版本为 3.8
PS D:\Users\86180\virtualenv> virtualenv cv2 --python=3.8
# 查看虚拟环境目录    
目录: D:\Users\86180\virtualenv


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        2022-01-05     10:47                cv2
d-----        2021-12-26     19:10                tf
# 跳转到指定环境的 Scripts 目录下，激活环境
PS D:\Users\86180\virtualenv\cv2\Scripts> .\activate
(cv2) PS D:\Users\86180\virtualenv\cv2\Scripts>
```

 ## 05.Django 项目

```shell
# 创建Django项目
django_admin startproject test

```

默认项目的文件介绍：

```shell
D:\DATABASE_SHKE_DEV\PYTHON\DJANGO\OIL_TEST
│  manage.py			【项目的管理、启动项目、创建APP、数据管理】 【慎用】
│
└─oil_test
        asgi.py			【项目配置】			【常用】
        settings.py		【URL和函数的对应关系】 【常用】
        urls.py			【接受网络请求】		【慎用】
        wsgi.py			【接受网络请求】		【慎用】
        __init__.py
```

APP的文件架构：

```shell
D:\DATABASE_SHKE_DEV\PYTHON\DJANGO\OIL_TEST
│  manage.py
│
├─app01
│  │  admin.py		【默认，不修改】 django提供了admin后台管理
│  │  apps.py		【默认，不修改】 app启动类
│  │  models.py		 【**重要**】 对数据库操作
│  │  tests.py		【默认，不修改】 单元测试
│  │  views.py		【**重要**】被调用 函数
│  │  __init__.py
│  │
│  └─migrations		【默认，不修改】 数据库变更记录
│          __init__.py
│
└─oil_test
    │  asgi.py
    │  settings.py
    │  urls.py		【URL-> 函数】
    │  wsgi.py
    │  __init__.py
    │
    └─__pycache__
            settings.cpython-310.pyc
            __init__.cpython-310.pyc
```

一般步骤

1. 注册APP【settings.py】

2. 编写URL和视图函数的对应关系 【urls.py】

3. 编写视图函数

4. 启动Django项目

   ```shell
   python manage.py runserver
   ```

### 06.MySQL

```shell
# 启动服务
net start MySQL
# 终止服务
net start MySQL
# 制作服务
mysqld --install mysql157

# 登录
mysql -u root -p
passwd: root

# 显示数据库
show databases;

# 创建
create database name DEFAULT CHARSET utf8 COLLATE utf8_generral_ci;
# 删除
drop database;
# 进入表
use name;
# 查看表信息
desc table_name;
# 查看表中的值
select * from table_name;

# 更改密码
alter user 'root'@'localhost' identifided by 'root'
```

#### Django 操作数据库

```python
# 在models.py新建一个类
class UserInfo(models.Model):
    name = models.CharField(max_length=32)
    password = models.CharField(max_length=64)
    age = models.ImageField()

'''
Django 将会自动在数据库创建一个表
create table app01_userinfo(
    id bigint auto_increment primary key,
    name varchar(32),
    password varchar(64),
    age int
)
'''
```

执行命令：

```shell
# app已注册
python manage.py makemigrations
python manage.py migrate
```

数据表的增删：

```python
# 直接增加会要求给出默认值
size = models.IntegerField()
# 给定默认值
age = models.IntegerField(default=2)
# 允许值为空
data = models.IntegerField(null=True, blank=True)
# 删除注释即可
```

QuerySet 对象

```python
__exact #精确等于 like 'aaa'
__iexact #精确等于 忽略大小写 ilike 'aaa'
__contains #包含 like '%aaa%'
__icontains #包含 忽略大小写 ilike '%aaa%'，但是对于sqlite来说，contains的作用效果等同于icontains。
__gt #大于
__gte #大于等于
__lt #小于
__lte #小于等于
__in #存在于一个list范围内
__startswith #以...开头
__istartswith #以...开头 忽略大小写
__endswith #以...结尾
__iendswith #以...结尾，忽略大小写
__range #在...范围内
__year #日期字段的年份
__month #日期字段的月份
__day #日期字段的日
__isnull=True/False

# 例如
Amodel.objects.filter(age__gt=20)
```

