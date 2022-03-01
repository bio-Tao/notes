
<!-- TOC -->

- [1. python基础](#1-python基础)
- [2. numpy](#2-numpy)
- [3. pandas](#3-pandas)
- [4. sklearn](#4-sklearn)
- [5. matplotlib](#5-matplotlib)
  - [5.1. 绘图风格、画布、子图设置](#51-绘图风格画布子图设置)
  - [5.2. 添加显著性标记](#52-添加显著性标记)
  - [5.3. 标题、轴、图列设置](#53-标题轴图列设置)
  - [5.4. 保存、显示图](#54-保存显示图)
  - [5.5. 中文显示](#55-中文显示)

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

## 5.2. 添加显著性标记
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
```

## 5.3. 标题、轴、图列设置
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
plt.yticks(fontsize=10)
# 设置当前x轴标签
plt.xlabel('X 轴',fontsize=13)
# 设置当前y轴标签
plt.ylabel('y 轴',fontsize=13)
# 设置图列
plt.legend(prop={'family':'SimHei','size':6})
# 添加网格
plt.grid(axis="y")
# 排版
plt.tight_layout()
```

## 5.4. 保存、显示图
```python
# 显示图
plt.show()
# 保存图
plt.savefig("path")
```

## 5.5. 中文显示
```python
# 全局中文
mpl.rcParams['font.family'] = 'SimHei'
# 解决中文显示负号问题
plt.rcParams['axes.unicode_minus'] = False
```