
<!-- TOC -->

- [1. python基础](#1-python基础)
- [2. numpy](#2-numpy)
- [3. pandas](#3-pandas)
  - [创建对象](#创建对象)
  - [查看数据](#查看数据)
  - [数据提取](#数据提取)
  - [缺失值处理](#缺失值处理)
  - [操作](#操作)
  - [读取和输出文件](#读取和输出文件)
- [4. sklearn](#4-sklearn)
- [5. matplotlib](#5-matplotlib)
  - [5.1. 绘图风格、画布、子图设置](#51-绘图风格画布子图设置)
  - [5.2. 绘图](#52-绘图)
  - [5.3. 添加标记、注释](#53-添加标记注释)
  - [5.4. 标题、轴、图列设置](#54-标题轴图列设置)
  - [5.5. 保存、显示图](#55-保存显示图)
  - [5.6. 中文显示](#56-中文显示)

<!-- /TOC -->

# 1. python基础
<div align=center>
    <img src="https://github.com/bio-Tao/notes/raw/main/%E5%9B%BE%E7%89%87/python%E9%80%9F%E6%9F%A5/Python%E9%80%9F%E6%9F%A5_python%E5%9F%BA%E7%A1%80.jpg" style="zoom: 100%;" />
</div>


# 2. numpy
<div align=center>
    <img src="https://github.com/bio-Tao/notes/raw/main/%E5%9B%BE%E7%89%87/python%E9%80%9F%E6%9F%A5/Python%E9%80%9F%E6%9F%A5_numpy.jpg" style="zoom: 100%;" />
</div>


# 3. pandas
<div align=center>
    <img src="https://github.com/bio-Tao/notes/raw/main/%E5%9B%BE%E7%89%87/python%E9%80%9F%E6%9F%A5/Python%E9%80%9F%E6%9F%A5_pandas-1.jpg" style="zoom: 100%;" />
    <img src="https://github.com/bio-Tao/notes/raw/main/%E5%9B%BE%E7%89%87/python%E9%80%9F%E6%9F%A5/Python%E9%80%9F%E6%9F%A5_pandas-2.jpg" style="zoom: 100%;" />
</div>

## 创建对象
```python
# 创建Series
s = pd.Series([1, 3, 5, np.nan, 6, 8])

# 创建DataFrame
df = pd.DataFrame(np.random.randn(6, 4), index=dates, columns=list("ABCD"))  # 通过NumPy array创建
df = pd.DataFrame(
    {
        "A": 1.0,
        "B": pd.Timestamp("20130102"),
        "C": pd.Series(1, index=list(range(4)), dtype="float32"),
        "D": np.array([3] * 4, dtype="int32"),
        "E": pd.Categorical(["test", "train", "test", "train"]),
        "F": "foo",
    }
   )  # 通过字典创建
```

## 查看数据
```python
# 每一列数据类型
df.dtypes
# 前十行
df.head()
# 后三行
df.tail(3)
# 数据索引
df.index
# 数据列名
df.columns
# 转为numpy array
df.to_numpy()
np.asarray(s)
# 每列数据摘要（如mean、std等）
df.describe()
# 转置
df.T
# 排序
df.sort_index(axis=1, ascending=False)  # 列名降序排列
df.sort_values(by="B")  # 通过某列值排序
```

## 数据提取
```python
# 提取列
df["A"]
df[["A","B"]]
# 根据标签切片[行,列]
df.loc[:, ["A", "B"]]
# 根据位置切片[行,列]
df.iloc[3:5, 0:2]
df.iloc[[1, 2, 4], [0, 2]]
# 提取某列>0的行
df[df["A"] > 0]
# 不满足位置值为NaN
df[df > 0]
# 使用isin提取
df2[df2["E"].isin(["two", "four"])]
```

## 缺失值处理
```python
# 删除有NaN值的所有行
df1.dropna(how="any")
# 使用新的值填充NaN值
df1.fillna(value=5)
# 判断所有值是否为空，并返回DataFrame
pd.isna(df1)
```

## 操作
```python
# 均值
df.mean()  # 列均值
df.mean(1)  # 行均值
# 减法
df1.sub(df2)
df.sub(s, axis=0)
df.sub(s, axis=1)
# 加法
df.add(df2, fill_value=0)

# 遍历所有Series进行操作
df.apply(np.cumsum)
df.apply(lambda x: x.max() - x.min())
# 对Series中元素计数
s.value_counts()
# Series中字符转为小写
s.str.lower()

# 纵向连接DataFrame对象（join='inner'--只合并相同列）
pd.concat([df1, df2], ignore_index=True)
# 横向连接DataFrame对象
pd.concat([df1, df4], axis=1)
# SQL style merges
pd.merge(left, right, on="key")

# 分组进行操作
df.groupby("A").sum()
# 数据类型转换
df.astype("int")
df["raw_grade"].astype("category")
```

## 读取和输出文件
```python
# 输出到excel
df.to_excel("foo.xlsx", sheet_name="Sheet1")
# 读取excel
pd.read_excel("foo.xlsx", "Sheet1", index_col=None, na_values=["NA"])
```

# 4. sklearn
<div align=center>
    <img src="https://github.com/bio-Tao/notes/raw/main/%E5%9B%BE%E7%89%87/python%E9%80%9F%E6%9F%A5/Python%E9%80%9F%E6%9F%A5_sklearn.jpg" style="zoom: 100%;" />
</div>


# 5. matplotlib
<div align=center>
    <img src="https://github.com/bio-Tao/notes/raw/main/%E5%9B%BE%E7%89%87/python%E9%80%9F%E6%9F%A5/Python%E9%80%9F%E6%9F%A5_matplotlib.jpg" style="zoom: 100%;" />
</div>

## 5.1. 绘图风格、画布、子图设置
```python
# 绘图风格
plt.style.available  # 所有绘图风格
plt.style.use('ggplot')

# 设置画布大小，dpi
plt.figure(figsize=(6, 4), dpi=300)

# 指定2行1列的子图布局，共享x、y轴
plt.subplots(2,1,figsize=(6, 4), dpi=300，sharex=True, sharey=True)

# 2行1列第一个位置绘图
plt.subplot(2, 1, 1)

# 图与画布上下左右距离，子图之间距离
subplots_adjust(left=None, bottom=None, right=None, top=None, wspace=None, hspace=None)
```

## 5.2. 绘图
```python
# 折线图
plt.plot(x,y,color="r",label='line 1',linewidth=2,linestyle="-")

# 柱状图
err_attr={"elinewidth":1,"ecolor":"black","capsize":3}  # 柱状图误差线
plt.bar(x,y,yerr=std,error_kw=err_attr,width=0.3,color='red',alpha=0.5,label='bar 1',align='center')

# 分组柱状图
plt.bar(x-width/2,y,yerr=std,error_kw=err_attr,width=width,color='red',alpha=0.5,label='bar 1',align='center')
plt.bar(x-width/2,y,yerr=std,error_kw=err_attr,width=width,color='red',alpha=0.5,label='bar 2',align='center')

# 添加误差线
plt.errorbar(x, y, std, color="k",capsize=3,capthick=1)
```

## 5.3. 添加标记、注释
```python
# 添加显著性P值线
def draw_P(x1,x2,y1,y2,text):
    """
    x1 : x轴方向开始位置
    x2 : x轴方向结束位置
    y1 : y轴方向开始位置
    y2 : y轴方向结束位置
    text : 添加的文本
    """
    plt.plot([x1,x1,x2,x2], [y1,y2,y2,y1], lw=1, c="k")
    plt.text((x1+x2)*.5, y2, text, ha='center',va='bottom', color="k",fontsize=5)

# 柱状图添加注释
def set_label(rects):
    """
    rects : 绘图区域[ =plt.bar() ]
    """
    for rect in rects:
        height = rect.get_height()  # 获取⾼度
        plt.text(x = rect.get_x() + rect.get_width()/2,  # ⽔平坐标
                 y = height + 0.5,  # 竖直坐标
                 s = height,  # ⽂本
                 ha = 'center')  # ⽔平居中
```

## 5.4. 标题、轴、图列设置
```python
# 设置主标题
plt.suptitle('My Figure',fontsize=10)
# 设置图标题
plt.title("the first picture",fontsize=10)

# 设置x轴长度
plt.xlim(0,2300)
# 设置y轴长度
plt.ylim(0,2300)
# 设置当前x轴刻度位置和标签
plt.xticks([index-0.705 for index in range(1,9)], df_circ["index"],fontsize=10)
# 设置当前y轴刻度位置和标签
plt.yticks(range(0,2600,500),fontsize=10)
# 设置当前x轴标签
plt.xlabel('X 轴',fontsize=13)
# 设置当前y轴标签
plt.ylabel('y 轴',fontsize=13)

# 设置图列
plt.legend(prop={'family':'SimHei','size':6})
# 添加网格
plt.grid(axis="y")
# 紧凑布局
plt.tight_layout()
```

## 5.5. 保存、显示图
```python
# 显示图
plt.show()
# 保存图
plt.savefig("path")
```

## 5.6. 中文显示
```python
# 全局中文
mpl.rcParams['font.family'] = 'SimHei'
# 解决中文显示负号问题
plt.rcParams['axes.unicode_minus'] = False
```