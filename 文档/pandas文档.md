<!-- TOC -->

- [1. 输入、输出](#1-%E8%BE%93%E5%85%A5%E8%BE%93%E5%87%BA)
    - [1.1. csv文件](#11-csv%E6%96%87%E4%BB%B6)
    - [1.2. excel文件](#12-excel%E6%96%87%E4%BB%B6)
- [2. 一般功能](#2-%E4%B8%80%E8%88%AC%E5%8A%9F%E8%83%BD)
    - [2.1. 数据操作](#21-%E6%95%B0%E6%8D%AE%E6%93%8D%E4%BD%9C)
    - [2.2. 缺失值](#22-%E7%BC%BA%E5%A4%B1%E5%80%BC)
    - [2.3. 转换为数字](#23-%E8%BD%AC%E6%8D%A2%E4%B8%BA%E6%95%B0%E5%AD%97)
- [3. DataFrame](#3-dataframe)
    - [3.1. 属性和基础数据](#31-%E5%B1%9E%E6%80%A7%E5%92%8C%E5%9F%BA%E7%A1%80%E6%95%B0%E6%8D%AE)
    - [3.2. 转换](#32-%E8%BD%AC%E6%8D%A2)
    - [3.3. 索引、迭代](#33-%E7%B4%A2%E5%BC%95%E8%BF%AD%E4%BB%A3)
    - [3.4. 二元运算符函数](#34-%E4%BA%8C%E5%85%83%E8%BF%90%E7%AE%97%E7%AC%A6%E5%87%BD%E6%95%B0)
    - [3.5. 计算/描述性统计](#35-%E8%AE%A1%E7%AE%97%E6%8F%8F%E8%BF%B0%E6%80%A7%E7%BB%9F%E8%AE%A1)
    - [3.6. Function application, GroupBy & window](#36-function-application-groupby--window)
    - [3.7. 重新索引、选择、对标签操作](#37-%E9%87%8D%E6%96%B0%E7%B4%A2%E5%BC%95%E9%80%89%E6%8B%A9%E5%AF%B9%E6%A0%87%E7%AD%BE%E6%93%8D%E4%BD%9C)
    - [3.8. 缺失数据处理](#38-%E7%BC%BA%E5%A4%B1%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86)

<!-- /TOC -->

# 1. 输入、输出

## 1.1. csv文件
```python
# 读取csv
pandas.read_csv(
        filepath_or_buffer,  # 文件路径 (str, path object or file-like object)
        sep=NoDefault.no_default,   # 分隔符 (str, default ",")
        header='infer',  # 用做列名的行，并作为数据开始的行 (int, list of int, None)
        names=NoDefault.no_default,  # 使用的列名列表 (array-like)
        index_col=None,  # 用作索引的列，index_col=False : 不指定索引 (int, str, sequence of int / str, or False)
        usecols=None,  # 提取出指定的列 (list-like or callable)
        squeeze=None,  # 设置为True则当数据只包含一列时，返回Series (bool, default False)
        prefix=NoDefault.no_default,  # 没有列名时，添加列名，如"X"，则列名为X0，X1，X2··· (str)
        mangle_dupe_cols=True,  # 是否重复列名被命名为X0，X1，如设置为False则被覆盖 (bool)
        dtype=None,  # 数据类型 (Type name or dict of column -> type)
        converters=None,  # 使用函数转换某些列中的值 (dict)
        skipinitialspace=False,  # 分隔符后是否跳过空格 (bool)
        skiprows=None,  # 跳过的行或忽略的行数 (list-like, int or callable)
        skipfooter=0,  # 文件底部要跳过的行数 (int, default 0)
        nrows=None,  # 要读取的行数 (int)
        na_values=None,  # 要识别为空值的字符 (scalar, str, list-like, or dict)
        keep_default_na=True,  # 是否启用默认识别为空值的字符 (bool)
        na_filter=True,  # 空值是否标记为字符，设置为False可提高读取大文件效率 (bool)
        verbose=False,  # 非数字列中的空值的数量 (bool)
        skip_blank_lines=True,  # 是否跳过空行 (bool)
        parse_dates=None,  # 解析日期 (bool or list of int or names or list of lists or dict, default False)
        infer_datetime_format=False,  # 如果设定为True并且parse_dates 可用，那么pandas将尝试转换为日期类型，如果可以转换，转换并解析 (bool)
        keep_date_col=False,  # 如果连接多列解析日期，则保留参与连接的列 (bool)
        date_parser=None,  # 将字符串列序列转换为日期时间的函数 (function)
        dayfirst=False,  # 是否启用DD/MM格式的日期 (bool)
        iterator=False,  # 返回 TextFileReader 对象以进行迭代或使用 get_chunk() 获取块，逐块处理文件 (bool)
        chunksize=None,  # 块的大小 (int)
        compression='infer',  # 直接读取压缩文件 (str or dict, default "infer")
        thousands=None,  # 千分位分隔符 (str)
        decimal='.',  # 识别为小数点的字符 (str, default ".")
        lineterminator=None,  # 将文件分成几行的字符 (str)
        comment=None,  # 使用字符标识行不被解析,仅为一个字符且在行首标记 (str)
        encoding=None  # 指定字符集编码类型 (str)
     )

# 输出csv
DataFrame.to_csv(
        path_or_buf=None,  # 输出文件路径 (str, path object, file-like object, or None)
        sep=',',  # 分隔符 (str, default ",")
        na_rep='',  # 缺失数据字符串表示 (str, default "")
        float_format=None,  # 浮点数的格式字符串 (str)
        columns=None,  # 要写入的列 (sequence)
        header=True,  # 是否写入列名或传入列名 (bool or list of str, default True)
        index=True,  # 是否写入索引名 (bool, default True)
        index_label=None,  # 索引列的列标签 (str or sequence, or False)
        mode='w',  # Python 写入模式 (str, default "w")
        encoding=None,  # 指定字符集编码类型 (str)
        compression='infer',  # 输出时压缩 (str or dict, default ‘infer’)
        line_terminator=None,  # 要在输出文件中使用的换行符或字符序列 (str)
        chunksize=None,  # 一次写入行数 (int or None)
        date_format=None,  # 日期时间对象的格式字符串 (str)
        decimal='.'  #识别为小数分隔符的字符 (str, default ".")
    )
```

## 1.2. excel文件
```python
# 读取excel
pandas.read_excel(
        io,  # 文件路径 (str, bytes, ExcelFile, xlrd.Book, path object, or file-like object)
        sheet_name=0,  # 表单名(str, int, list, or None, default 0)
        header=0,  # 用第几行作为表头 (int, list of int, default 0)
        names=None,  # 使用的列名列表 (array-like)
        index_col=None,  # 用作索引的列 (int, list of int)
        usecols=None,  # 提取出指定的列 (int, str, list-like, or callable default None)
        squeeze=None,  # 设置为True则当数据只包含一列时，返回Series (bool, default False)
        dtype=None,  # 数据类型 (Type name or dict of column -> type)
        converters=None,  # 使用函数转换某些列中的值 (dict)
        true_values=None,  # 将指定的文本转换为True (list)
        false_values=None,  # 将指定的文本转换为False (list)
        skiprows=None,  # 跳过的行或忽略的行数 (list-like, int or callable)
        nrows=None,  # 要读取的行数 (int)
        na_values=None,  # 要识别为空值的字符 (scalar, str, list-like, or dict)
        keep_default_na=True,  # 是否启用默认识别为空值的字符 (bool)
        na_filter=True,  # 空值是否标记为字符，设置为False可提高读取大文件效率 (bool)
        verbose=False,  # 非数字列中的空值的数量 (bool)
        parse_dates=False,  # 解析日期 (bool or list of int or names or list of lists or dict, default False)
        date_parser=None,  # 将字符串列序列转换为日期时间的函数 (function)
        thousands=None,  # 千分位分隔符 (str)
        decimal='.',  # 识别为小数点的字符 (str, default ".")
        comment=None,  # 使用字符标识行不被解析,仅为一个字符且在行首标记 (str)
        skipfooter=0,  # 文件底部要跳过的行数 (int, default 0)
        convert_float=None,  # 将整数浮点数转换为int (bool)
        mangle_dupe_cols=True  # 重复列是否被指定为X.1、X.2··· (bool)
    )

# 输出excel
DataFrame.to_excel(
        excel_writer,  # 文件路径 (path-like, file-like, or ExcelWriter object)
        sheet_name='Sheet1',  # 表单名 (str, default "Sheet1")
        na_rep='',  # 缺失数据字符串表示 (str, default "")
        float_format=None,  # 浮点数的格式字符串 (str)
        columns=None,  # 要写入的列 (sequence or list of str)
        header=True,  # 是否写入列名或指定列名 (bool or list of str, default True)
        index=True,  # 是否写入索引 (bool, default True)
        index_label=None,  # 索引列的列标签(str or sequence, optional)
        encoding=None,  # 指定字符集编码类型 (str)
        inf_rep='inf',  # 无穷大的表示 (str, default "inf")
        freeze_panes=None  # 用于指定要冻结的最底部一行和最右边一列 (tuple of int (length 2))
    )
```

# 2. 一般功能

## 2.1. 数据操作
```python
# 将 DataFrame 从宽格式转为长格式
DataFrame.melt
pandas.melt(
        frame,  # data
        id_vars=None,  # 用作标识符变量的列 (tuple, list, or ndarray)
        value_vars=None,  # 需要转换的列名 (tuple, list, or ndarray)
        var_name=None,  # 用于“变量”列的名称 (scalar)
        value_name='value',  # 用于“值”列的名称 (scalar)
        ignore_index=True # 是否忽略原始索引 (bool)
    )

# 返回给定索引、列值的DataFrame
pandas.pivot(
        data,  # DataFrame
        index=None,  # 新DataFrame的索引 (str or object or a list of str)
        columns=None,  # 新DataFrame的列名 (str or object or a list of str)
        values=None # 新DataFrame的值使用哪些列 (str, object or a list of the previous)
    )

# 将值分类为离散间隔
pandas.cut(
        x,  # 要分箱的输入数组。必须是一维的 (array-like)
        bins,  # 分箱数，每一个bin的区间边缘，精确区间 (int, sequence of scalars, or IntervalIndex)
        right=True,  # bin是否包含区间右部 (bool)
        labels=None,  # bin的标签 (array or False)
        retbins=False,  # 是否将分割后的bins返回 (bool)
        precision=3,  # 存储和显示 bin 标签的精度 (int)
        include_lowest=False,  # 区间的左边是开还是闭的 (bool)
        duplicates='raise',  # 是否允许重复区间 (raise：不允许，drop：允许)
        ordered=True  # 标签是否有序 (bool)
    )

# 按数量分箱
pandas.qcut(
        x,  # 要分箱的输入数组。必须是一维的 (array-like)
        q,  # 分位数 (int or list-like of float)
        labels=None,  # bin的标签 (array or False)
        retbins=False,  # 是否将分割后的bins返回 (bool)
        precision=3,  # 存储和显示 bin 标签的精度 (int)
        duplicates='raise')  # 是否允许重复区间 (raise：不允许，drop：允许)

# 将 DataFrame 或命名的 Series 对象连接合并
pandas.merge(
        left,  # DataFrame
        right,  # 要合并的对象 (DataFrame or named Series)
        how='inner',  # 要执行的合并类型 ("left", "right", "outer", "inner", "cross")
        on=None,  # 用于连接的列或索引名 (label or list)
        left_on=None,  # 左侧用于连接的列或索引名 (label or list, or array-like)
        right_on=None,  # 右侧用于连接的列或索引名 (label or list, or array-like)
        left_index=False,  # 使用左侧 DataFrame 中的索引作为连接键 (bool)
        right_index=False,  # 使用右侧 DataFrame 中的索引作为连接键 (bool)
        sort=False,  # 根据连接键进行排序 (bool)
        suffixes=('_x', '_y'),  # 添加到左右重叠列名的后缀 (list-like)
        copy=True,  # 是否复制 (bool)
        indicator=False,  # 是否输出每行来源信息 (bool)
        validate=None  # 检查合并是否属于指定类型 ("1:1","1:m","m:1","m:m")
    )

# 沿特定轴连接 pandas 对象
pandas.concat(
        objs, # data (a sequence or mapping of Series or DataFrame objects)
        axis=0,  # 要连接的轴
        join='outer',  # 处理方式 ("outer","inner")
        ignore_index=False,  # 是否不要沿连接轴使用索引值 (bool)
        keys=None  # 使用传递的键作为最外层构建层次索引 (sequence)
    )

# 将分类变量转变为虚拟/指标变量(独热编码)
pandas.get_dummies(
        data,  # data (array-like, Series, or DataFrame)
        prefix=None,  # 附加 DataFrame 列名的字符串 (str, list of str, or dict of str)
        prefix_sep='_',  # 如果附加前缀，则使用分隔符/定界符 (str)
        dummy_na=False,  # 如果忽略 False NaN，则添加一列以指示 NaN (bool)
        columns=None,  # 要编码的 DataFrame 中的列名 (list-like)
        drop_first=False,  # 是否通过删除第一级从 k 个分类级别中取出 k-1 个虚拟变量 (bool)
        dtype=None  # 新列的数据类型 (dtype)
    )

# 将对象编码为枚举类型或分类变量，映射为一组数字
pandas.factorize(
        values,  # data (sequence)
        sort=False,  # 表示是否对unique进行排序 (bool)
        na_sentinel=- 1, 
        size_hint=None
    )

# 返回唯一值
pandas.unique(values)  # 1d array-like

# 将 DataFrame 从宽格式转为长格式
pandas.wide_to_long(
        df,  # DataFrame
        stubnames,  # 提取以指定字符串开头的列 (str or list-like)
        i,  # 用作索引的列 (str or list-like)
        j,  # 提取开头后剩余的部分会成一列，在此指定列名 (str)
        sep='',  # 分隔符 (str)
        suffix='\\d+'  # 捕获正则表达式匹配的后缀 (str)
    )
```

## 2.2. 缺失值
```python
# 检查是否为空值
pandas.isna(obj)
pandas.isnull(obj)

# 检查是否为非空值
pandas.notna(obj)
pandas.notnull(obj)
```

## 2.3. 转换为数字
```python
# 将参数转换为数值类型
pandas.to_numeric(
        arg,  # data (scalar, list, tuple, 1-d array, or Series)
        errors='raise'  # 忽然无效解析，无效解析引发异常，无效解析转化为空值 ("ignore", "raise", "coerce")
    )
```

# 3. DataFrame

## 3.1. 属性和基础数据
```python
# DataFrame 的索引
DataFrame.index
# DataFrame 的列名
DataFrame.columns
# 每列的数据类型
DataFrame.dtypes

# 打印 DataFrame 的简明摘要
DataFrame.info(
        verbose=None,  # 是否打印完整的摘要 (bool)
        buf=None,  
        max_cols=None,  
        memory_usage=None,  # 是否应显示DataFrame元素(包括索引)的总内存使用情况 (bool, str)
        show_counts=None,  # 是否显示非空计数 (bool)
        null_counts=None
    )

# 根据列 dtypes 返回 DataFrame 列的子集
DataFrame.select_dtypes(
        include=None,  # 是否包含 (bool)
        exclude=None  # 是否排除 (bool)
    )

# 返回 DataFrame 的 Numpy 表示 
DataFrame.values  # 建议使用 DataFrame.to_numpy()
# 返回一个表示轴数/数组维数的 int
DataFrame.ndim
# 返回一个表示此对象中元素数量的 int
DataFrame.size
# 返回一个表示 DataFrame 维度的元组
DataFrame.shape

# 返回每列的内存使用量
DataFrame.memory_usage(
        index=True,  # 是否在返回的 Series 中包含 DataFrame 索引的内存使用情况 (bool)
        deep=False  # 是否不object 类型系统级内存消耗 (bool)
    )

# 指示 Series/DataFrame 是否为空
DataFrame.empty  # 存在任何一个维度为0才返回True
```

## 3.2. 转换
```python
# 将 pandas 对象转换为指定的 dtype
DataFrame.astype(
        dtype,  # 需要转换的类型 (data type, or dict of column name -> data type)
        copy=True, # 是否返回副本 (bool)
        errors='raise' # 许引发异常，忽略异常返回原值 ("raise", "ignore")
    )

# 更改为最佳数据类型
DataFrame.convert_dtypes(
        infer_objects=True,  # 是否将对象数据类型转换为最佳数据类型
        convert_string=True,  # 是否将对象数据类型转换为字符串
        convert_integer=True,  # 是否将对象数据类型转换为整数
        convert_boolean=True,  # 是否将对象数据类型转换为整数
        convert_floating=True  # 是否将对象数据类型转换为浮动类型
    )

# 尝试为对象列推断更好的 dtype
DataFrame.infer_objects()

# 复制
DataFrame.copy(deep=True)  # 是否为浅拷贝，Fasle--浅拷贝

# 判断单个bool值
DataFrame.bool()
```

## 3.3. 索引、迭代
```python
# 查看前 n 行
DataFrame.head(n=5)
# 查看后 n 行
DataFrame.tail(n=5)
# 基于标签访问单个值
DataFrame.at
# 基于位置的索引访问单个值
DataFrame.iat
# 通过标签或布尔数组访问一组行和列
DataFrame.loc
# 基于整数位置的索引，用于按位置进行选择
DataFrame.iloc

# 在指定位置将列插入 DataFrame
DataFrame.insert(
        loc,  # 插入索引 (int)
        column,  # 插入列的标签 (str, number, or hashable object)
        value,  # 插入列的值 (Scalar, Series, or array-like)
        allow_duplicates=False  # 是否允许重复
    )

# 遍历 DataFrame 列，返回一个包含列名和内容的元组作为一个系列
DataFrame.__iter__()
DataFrame.iteritems()

# 获取索引
DataFrame.keys()

# 将 DataFrame 行作为 (index, Series) 对进行迭代
DataFrame.iterrows()

# 以命名元组的形式迭代 DataFrame
DataFrame.itertuples(
        index=True,  # 是否行迭代 (bool)
        name='Pandas'  # 命名元组的名称 (str or None)
    )

# 删除列
DataFrame.pop(item)  # 列标签 (label)

# 获取给定键的对象
DataFrame.get(
        key,  # 给定的键
        default=None  # 未找到则返回的值
    )

# DataFrame 中的每个元素是否包含在值中
DataFrame.isin(values)  # (iterable, Series, DataFrame or dict)

# 替换条件为 False 的值
DataFrame.where(
        cond,  # 替换条件 (bool Series/DataFrame, array-like, or callable)
        other=nan,  # 要替换的值 (scalar, Series/DataFrame, or callable)
        inplace=False,  # 是否对数据直接操作 (bool)
        axis=None  # 轴方向 ()
    )
# 替换条件为 True 的值
DataFrame.mask(
        cond,  # 替换条件 (bool Series/DataFrame, array-like, or callable)
        other=nan,  # 要替换的值 (scalar, Series/DataFrame, or callable)
        inplace=False,  # 是否对数据直接操作 (bool)
        axis=None,  # 轴方向 ()
        level=None, 
        errors='raise', 
        try_cast=NoDefault.no_default)

# 使用布尔表达式查询 DataFrame 的列
DataFrame.query(
        expr,  # 查询表达式 (str)
        inplace=False,  # 是否对数据直接操作 (bool)
        **kwargs  
    )
```

## 3.4. 二元运算符函数
```python
# 加法
DataFrame.add(
        other, 
        axis='columns',  # 轴方向
        level=None, 
        fill_value=None  # 计算前填充空值 (float or None)
    )  # DataFrame + other
# 减法
DataFrame.sub(other, axis='columns', level=None, fill_value=None)
# 乘法
DataFrame.mul(other, axis='columns', level=None, fill_value=None)
# 浮点数除法
DataFrame.div(other, axis='columns', level=None, fill_value=None)
DataFrame.truediv(other, axis='columns', level=None, fill_value=None)
# 整数除法
DataFrame.floordiv(other, axis='columns', level=None, fill_value=None)
# 模运算
DataFrame.mod(other, axis='columns', level=None, fill_value=None)
# 指数运算
DataFrame.pow(other, axis='columns', level=None, fill_value=None)
# 矩阵乘法
DataFrame.dot(other)
# 前后交换加法 
DataFrame.radd(other, axis='columns', level=None, fill_value=None)  # other + DataFrame
# 前后交换减法 
DataFrame.rsub(other, axis='columns', level=None, fill_value=None)
# 前后交换乘法
DataFrame.rmul(other, axis='columns', level=None, fill_value=None)
# 前后交换浮点数除法
DataFrame.rdiv(other, axis='columns', level=None, fill_value=None)
DataFrame.rtruediv(other, axis='columns', level=None, fill_value=None)
# 前后交换整数除法
DataFrame.rfloordiv(other, axis='columns', level=None, fill_value=None)
# 前后交换取模运算
DataFrame.rmod(other, axis='columns', level=None, fill_value=None)
# 前后交换指数运算
DataFrame.rpow(other, axis='columns', level=None, fill_value=None)

# 判断是否小于DataFrame
DataFrame.lt(other, axis='columns', level=None)
# 判断是否大于DataFrame
DataFrame.gt(other, axis='columns', level=None)
# 判断是否小于等于DataFrame
DataFrame.le(other, axis='columns', level=None)
# 判断是否大于等于DataFrame
DataFrame.ge(other, axis='columns', level=None)
# 判断是否不等于DataFrame
DataFrame.ne(other, axis='columns', level=None)
# 判断是否等于DataFrame
DataFrame.eq(other, axis='columns', level=None)

# DataFrame按列组合，索引和列名为两个DataFrame的并集
DataFrame.combine(
        other,  # DataFrame
        func,  # 用于逐列合并两个数据框的函数
        fill_value=None,  # 计算前填充空值 (float or None)
        overwrite=True  # 如果为 True，则 self 中不存在于 other 中的列将被 NaN 覆盖
    )
# 使用其他相同位置的值更新NaN
DataFrame.combine_first(other)
```

## 3.5. 计算/描述性统计
```python
# 绝对值
DataFrame.abs()

# 是否所有元素都为真
DataFrame.all(
        axis=0,  # 轴方向 (0 or "index", 1 or "columns")
        bool_only=None,  # 仅包含布尔列 (bool)
        skipna=True,  # 是否排除 NaN (bool)
        level=None, 
        **kwargs
    )

# 是否有任何元素为真
DataFrame.any(
        axis=0,  # 轴方向 (0 or "index", 1 or "columns")
        bool_only=None,  # 仅包含布尔列 (bool)
        skipna=True,   # 是否排除 NaN (bool)
        level=None, 
        **kwargs
    )

# 将值限制在阈值
DataFrame.clip(
        lower=None,  # 最小阈值 (float or array-like)
        upper=None,  # 最大阈值 (float or array-like)
        axis=None,   # 轴方向 (0 or "index", 1 or "columns")
        inplace=False,  # 是否对数据直接操作 (bool)
        *args, 
        **kwargs
    )

# DataFrame的列之间的相关性
DataFrame.corr(
        method='pearson',  # 使用方法 ("pearson", "kendall", "spearman") 
        min_periods=1   # 最少数据量 (int)
    )

# DataFrame与other的列或行相关性
DataFrame.corrwith(
        other,  # DataFrame, Series 
        axis=0,   # 轴方向 (0 or "index", 1 or "columns")
        drop=False,  # 从结果中删除缺失的索引 (bool)
        method='pearson'  # 使用方法 ("pearson", "kendall", "spearman") 
    )

# 计算行或列的非空元素个数
DataFrame.count(
        axis=0,  # 轴方向 (0 or "index", 1 or "columns")
        level=None,  
        numeric_only=False  # 是否仅包括浮点、整数或布尔数据 (bool)
    )

# DataFrame的列之间的协方差
DataFrame.cov(
        min_periods=None,  # 最少数据量 (int)
        ddof=1  # Delta 自由度，计算中使用的除数 N - ddof
    )

# 延轴累计最大值
DataFrame.cummax(
        axis=None,  # 轴方向 (0 or "index", 1 or "columns")
        skipna=True,  # 是否排除 NaN 空值 (bool)
        *args, 
        **kwargs
    )
# 延轴累计最小值
DataFrame.cummin(
        axis=None,  # 轴方向 (0 or "index", 1 or "columns")
        skipna=True,  # 是否排除 NaN 空值 (bool)
        *args, 
        **kwargs
    )
# 延轴累乘
DataFrame.cumprod(
        axis=None,  # 轴方向 (0 or "index", 1 or "columns")
        skipna=True,  # 是否排除 NaN 空值 (bool)
        *args, 
        **kwargs
    )
# 延轴累加
DataFrame.cumsum(
        axis=None,  # 轴方向 (0 or "index", 1 or "columns")
        skipna=True,  # 是否排除 NaN 空值 (bool)
        *args, 
        **kwargs
    )

# 生成描述性统计数据
DataFrame.describe(
        percentiles=None,  # 输出中的百分位数 (list-like of numbers, default [.25, .5, .75])
        include=None,  # 包含在结果中的数据类型白名单 ("all", list-like of dtypes or None (default))
        exclude=None,  # 排除在结果中的数据类型白名单 ("all", list-like of dtypes or None (default))
        datetime_is_numeric=False  # 是否将 datetime dtypes 视为数字 (bool)
    )

# 延轴计算 Dataframe 元素与 Dataframe 中另一个元素的差异
DataFrame.diff(
        periods=1,  # 用于计算差异的步长，接受负值 (int)
        axis=0  # 轴方向 (0 or "index", 1 or "columns")
    )

# 对列进行表达式操作
DataFrame.eval(
        expr,  # 要计算的表达式字符串 (str)
        inplace=False,  # 是否对数据直接操作 (bool)
        **kwargs
    )

# 指定轴的无偏峰度
DataFrame.kurt(
        axis=NoDefault.no_default,  # 轴方向 (0 or "index", 1 or "columns")
        skipna=True,  # 计算结果时是否排除 NaN 值 (bool)
        level=None, 
        numeric_only=None,  # 是否仅包括浮点、整数或布尔数据 (bool)
        **kwargs
    )
DataFrame.kurtosis(axis=NoDefault.no_default, skipna=True, level=None, numeric_only=None, **kwargs)
# 指定轴的无偏偏态（偏度）
DataFrame.skew(
        axis=NoDefault.no_default,  # 轴方向 (0 or "index", 1 or "columns")
        skipna=True,  # 计算结果时是否排除 NaN 值 (bool)
        level=None, 
        numeric_only=None,  # 是否仅包括浮点、整数或布尔数据 (bool)
        **kwargs
    )
# 指定轴的平均绝对偏差
DataFrame.mad(
        axis=None,  # 轴方向 (0 or "index", 1 or "columns")
        skipna=True,  # 计算结果时是否排除 NaN 值 (bool)
        level=None
    )
# 指定轴的最大值
DataFrame.max(
        axis=NoDefault.no_default,  # 轴方向 (0 or "index", 1 or "columns")
        skipna=True,  # 计算结果时是否排除 NaN 值 (bool)
        level=None, 
        numeric_only=None,  # 是否仅包括浮点、整数或布尔数据 (bool)
        **kwargs
    )
# 指定轴的中位数
DataFrame.median(
        axis=NoDefault.no_default,  # 轴方向 (0 or "index", 1 or "columns")
        skipna=True,  # 计算结果时是否排除 NaN 值 (bool)
        level=None, 
        numeric_only=None,  # 是否仅包括浮点、整数或布尔数据 (bool)
        **kwargs
    )
# 指定轴的最小值
DataFrame.median(
        axis=NoDefault.no_default,  # 轴方向 (0 or "index", 1 or "columns")
        skipna=True,  # 计算结果时是否排除 NaN 值 (bool)
        level=None, 
        numeric_only=None,  # 是否仅包括浮点、整数或布尔数据 (bool)
        **kwargs
    )
# 指定轴的众数
DataFrame.mode(
        axis=0,  # 轴方向 (0 or "index", 1 or "columns")
        numeric_only=False,  # 是否仅包括浮点、整数或布尔数据 (bool)
        dropna=True  # 是否不考虑NaN (bool)
    )
# 指定轴的乘积
DataFrame.prod(
        axis=None,  # 轴方向 (0 or "index", 1 or "columns")
        skipna=True,  # 计算结果时是否排除 NaN 值 (bool)
        level=None, 
        numeric_only=None,  # 是否仅包括浮点、整数或布尔数据 (bool)
        min_count=0,  # 执行操作所需的有效值数 (int)
        **kwargs
    )
DataFrame.product(axis=None, skipna=True, level=None, numeric_only=None, min_count=0, **kwargs)
# 指定轴的和
DataFrame.sum(
        axis=None,  # 轴方向 (0 or "index", 1 or "columns")
        skipna=True,  # 计算结果时是否排除 NaN 值 (bool)
        level=None, 
        numeric_only=None,  # 是否仅包括浮点、整数或布尔数据 (bool)
        min_count=0,  # 执行操作所需的有效值数 (int)
        **kwargs
    )
# 指定轴的标准差
DataFrame.std(
        axis=None,  # 轴方向 (0 or "index", 1 or "columns")
        skipna=True,  # 计算结果时是否排除 NaN 值 (bool)
        level=None, 
        ddof=1,  # Delta 自由度，计算中使用的除数 N - ddof
        numeric_only=None,  # 是否仅包括浮点、整数或布尔数据 (bool)
        **kwargs
    )
# 指定轴的方差
DataFrame.var(
        axis=None,  # 轴方向 (0 or "index", 1 or "columns")
        skipna=True,  # 计算结果时是否排除 NaN 值 (bool)
        level=None, 
        ddof=1,  # Delta 自由度，计算中使用的除数 N - ddof
        numeric_only=None,  # 是否仅包括浮点、整数或布尔数据 (bool)
        **kwargs
    )
# 指定轴的平均值的无偏标准误差
DataFrame.sem(
        axis=None,  # 轴方向 (0 or "index", 1 or "columns")
        skipna=True,  # 计算结果时是否排除 NaN 值 (bool)
        level=None, 
        ddof=1,  # Delta 自由度，计算中使用的除数 N - ddof
        numeric_only=None,   # 是否仅包括浮点、整数或布尔数据 (bool)
        **kwargs
    )
# 指定轴的分位数
DataFrame.quantile(
        q=0.5,  # 分位数 (float or array-like)
        axis=0,  # 轴方向 (0 or "index", 1 or "columns")
        numeric_only=True,  # 是否仅包括浮点、整数或布尔数据 (bool)
        interpolation='linear'  # 分位数位于两点之间时，指定插值方法("linear", "lower", "higher", "midpoint", "nearest")
    )
# 指定轴的数据等级（1 到 n）
DataFrame.rank(
        axis=0,  # 轴方向 (0 or "index", 1 or "columns")
        method='average',  # 如何对相同值的记录组进行排名 ("average", "min", "max", "first", "dense")
        numeric_only=NoDefault.no_default,  # 是否仅包括浮点、整数或布尔数据 (bool)
        na_option='keep',  # 如何对 NaN 值进行排名 ("keep", "top", "bottom")
        ascending=True,  # 是否升序排列 (bool)
        pct=False # 是否以百分位形式显示返回的排名 (bool)
    )
# 指定轴的不同元素的数量
DataFrame.nunique(
        axis=0,  # 轴方向 (0 or "index", 1 or "columns")
        dropna=True  # 是否不考虑NaN (bool)
    )
# 唯一行的数量
DataFrame.value_counts(
        subset=None,  # 计算唯一组合时要使用的列 (list-like)
        normalize=False,  # 是否返回比率 (bool)
        sort=True,  # 是否按频率排序 (boll)
        ascending=False,  # 是否升序排列 (bool)
        dropna=True  # 是否不考虑NaN (bool)
    )

# 与前一行的百分比变化
DataFrame.pct_change(
        periods=1,  # 用于计算差异的步长，接受负值 (int)
        fill_method='pad',  # 如何处理NaN (str)
        limit=None,  # 停止前要填充的连续 NA 的数量 (int)
        freq=None,  # 时间序列的增量 (DateOffset, timedelta, or str)
        **kwargs
    )

# 每列保留小数位数
DataFrame.round(
        decimals=0, # 每列四舍五入的小数位数 (int, dict, Series)
        *args, 
        **kwargs
    )
```

## 3.6. Function application, GroupBy & window
```python
# 沿 DataFrame 的轴应用函数
DataFrame.apply(
        func,  # 应用于每一列或每一行的函数 (function)
        axis=0,  # 轴方向 (0 or "index", 1 or "columns")
        raw=False,  
        result_type=None, 
        args=(), 
        **kwargs
    )

# 将函数应用于 Dataframe 元素
DataFrame.applymap(
        func,  # Python 函数，从单个值返回单个值
        na_action=None, # 传递NaN (None, "ignore")
        **kwargs
    )

# 管道函数，链式编程
DataFrame.pipe(func, *args, **kwargs)

# 使用在指定轴上使用一个或多个操作聚合
DataFrame.agg(
        func=None,  # 用于聚合数据的功能 (function, str, list or dict)
        axis=0,  # 轴方向 (0 or "index", 1 or "columns")
        *args,  # 传给函数的位置参数 ()
        **kwargs
    )
DataFrame.aggregate(func=None, axis=0, *args, **kwargs)

# 将函数应用并，生成具有相同轴形状的DataFrame
DataFrame.transform(
        func,  # 用于转换数据的功能
        axis=0,  # 轴方向 (0 or "index", 1 or "columns")
        *args, 
        **kwargs
    )

# 分组
DataFrame.groupby(
        by=None,  # 用于确定GroupBy的组 (mapping, function, label, or list of labels)
        axis=0,  # 轴方向 (0 or "index", 1 or "columns")
        level=None,  
        as_index=True, 
        sort=True,  # 是否排序组键 (bool)
        group_keys=True,  # 调用apply时，将组键添加到索引用于识别 (bool)
        squeeze=NoDefault.no_default, 
        observed=False,  # 显示分类的观测值:True/所有值:False (bool)
        dropna=True  # 是否考虑NaN (bool)
    )

# 滑窗
DataFrame.rolling(
        window,  # 滑窗大小 (int, offset, or BaseIndexer subclass)
        min_periods=None,  # 最少需要有值的观测点的数量 (int, default None)
        center=False,  # 将窗口标签设置为窗口索引的中间 (bool)
        win_type=None,  # 窗口的类型,截取窗的各种函数
        on=None,  # 用于计算滚动窗口的列标签或索引 (str)
        axis=0,  # 轴方向 (0 or "index", 1 or "columns")
        closed=None,  # 区间的开闭 ("right","left","both","neither"," None"=="right")
        method='single'  # 单列或表执行滑窗 ("single", "table")
    )

# 滑窗并累计
DataFrame.expanding(min_periods=1, center=None, axis=0, method='single')  # 参数同 .rolling()

# 指数权重滑窗
DataFrame.ewm(
        com=None, 
        span=None, 
        halflife=None, 
        alpha=None, 
        min_periods=0, 
        adjust=True, 
        ignore_na=False, 
        axis=0, 
        times=None, 
        method='single'
    )  # 必须提供一个参数：com、span、halflife 或 alpha
```

## 3.7. 重新索引、选择、对标签操作
```python
# 标签加前缀
DataFrame.add_prefix(prefix)
# 标签加后缀
DataFrame.add_suffix(suffix)

# 将轴上的两个对象与每个轴索引以方法连接
DataFrame.align(
        other,  # DataFrame or Series
        join='outer',  # 连接方法 ("outer", "inner", "left", "right")
        axis=None,  # 轴方向 (0 or "index", 1 or "columns")
        level=None, 
        copy=True,  # 是否返回新对象 (bool)
        fill_value=None,  # 用于缺失值的值 (scalar)
        method=None,  
        limit=None, 
        fill_axis=0, 
        broadcast_axis=None
    )
# 选择一天中特定时间的值
DataFrame.at_time(time, asof=False, axis=None)
# 选择一天中特定时间之间的值
DataFrame.between_time(
        start_time, 
        end_time, 
        include_start=NoDefault.no_default, 
        include_end=NoDefault.no_default, 
        inclusive=None, 
        axis=None
    )

# 删除指定的行或列
DataFrame.drop(
        labels=None,  # 要删除的索引或列标签 (single label or list-like)
        axis=0,  # 轴方向 (0 or "index", 1 or "columns")
        index=None,  # 指定轴的替代方法 (single label or list-like)
        columns=None,  # 指定轴的替代方法 (single label or list-like)
        level=None,  
        inplace=False,  # 是否对数据直接操作 (bool)
        errors='raise' 
    )
# 删除重复行
DataFrame.drop_duplicates(
        subset=None,  # 仅考虑某些列来识别重复项 (column label or sequence of labels)
        keep='first',  # 确定要保留哪些重复项 ({"first", "last", False)
        inplace=False,  # 是否对数据直接操作 (bool)
        ignore_index=False
    )
# 表示重复行的布尔值
DataFrame.duplicated(
        subset=None,  # 仅考虑某些列来识别重复项 (column label or sequence of labels)
        keep='first'  # 哪条重复值标记为True ({"first", "last", False)
    )

# 两个对象是否包含相同的元素
DataFrame.equals(other)  # 忽略列名

# 根据指定的索引标签对数据框行或列取子集
DataFrame.filter(
        items=None,  # 保留项目中的轴标签 (list-like)
        like=None,  # 模糊匹配 (str)
        regex=None,  # 正则匹配 (str (regular expression))
        axis=None  # 轴方向 (0 or "index", 1 or "columns")
    )

# 根据日期偏移选择时间序列数据的初始期间
DataFrame.first(offset)  # 将选择的数据的偏移长度 (str, DateOffset or dateutil.relativedelta)
# 根据日期偏移选择时间序列数据的最终期间
DataFrame.last(offset)

# 返回前几行
DataFrame.head(n=5)
# 返回后几行
DataFrame.tail(n=5)
# 请求轴上第一次出现最大值的索引
DataFrame.idxmax(
        axis=0,  # 轴方向 (0 or "index", 1 or "columns")
        skipna=True  # 排除空值 (bool)
    )
# 请求轴上第一次出现最小值的索引
DataFrame.idxmin(
        axis=0,  # 轴方向 (0 or "index", 1 or "columns")
        skipna=True  # 排除空值 (bool)
    )
# 为series和dataframe添加或者删除索引
DataFrame.reindex(
        labels=None, 
        index=None, 
        columns=None, 
        axis=None, 
        method=None, 
        copy=True, 
        level=None, 
        fill_value=nan, 
        limit=None, 
        tolerance=None
    )
#  两个data进行索引匹配，返回一个具有匹配索引的对象
DataFrame.reindex_like(
        other, 
        method=None, 
        copy=True, 
        limit=None, 
        tolerance=None
    )
# 更改轴标签
DataFrame.rename(
        mapper=None,  # 更改轴标签 (dict-like or function)
        *, 
        index=None,  # 更改索引 (dict-like or function)
        columns=None,  # 更改列标签 (dict-like or function)
        axis=None,  # 轴方向 (0 or "index", 1 or "columns")
        copy=True,   # 是否返回新对象 (bool)
        inplace=False,  # 是否对数据直接操作 (bool)
        level=None, 
        errors='ignore'
    )
# 为索引或列设置轴的名称
DataFrame.rename_axis(
        mapper=None,  # 轴名称属性的值 (scalar, list-like)
        index=None,  # 索引轴名称 (scalar, list-like, dict-like or function)
        columns=None,  # 列轴名称 (scalar, list-like, dict-like or function)
        axis=None,  # 轴方向 (0 or "index", 1 or "columns")
        copy=True,  # 是否返回新对象 (bool)
        inplace=False  # 是否对数据直接操作 (bool)
    )
# 重置索引
DataFrame.reset_index(
        level=None, 
        drop=False, 
        inplace=False, 
        col_level=0, 
        col_fill=''
    )
# 抽样
DataFrame.sample(
        n=None,  # 样本数 (int)
        frac=None,  # 样本占比 (float)
        replace=False,  # 是否允许多次采样 (bool)
        weights=None,  # 权重 (str or ndarray-like)
        random_state=None,  # 随机数种子 (int, array-like, BitGenerator, np.random.RandomState)
        axis=None,  # 轴方向 (0 or "index", 1 or "columns")
        ignore_index=False
    )
# 更改列或行标签的索引
DataFrame.set_axis(
        labels,  # 新标签的值 (list-like)
        axis=0,  # 轴方向 (0 or "index", 1 or "columns")
        inplace=False  # 是否对数据直接操作 (bool)
    )
# 使用现有列设置 DataFrame 索引
DataFrame.set_index(
        keys,  # 列名 (label or array-like or list of labels/arrays)
        drop=True,  # 是否删除要用作新索引的列 (bool)
        append=False,  # 是否将索引添加到列 (bool)
        inplace=False,  # 是否对数据直接操作 (bool)
        verify_integrity=False  # 是否检查新索引是否重复 (bool)
    )
# 根据位置索引元素
DataFrame.take(
        indices, # 位置 (array-like)
        axis=0,  # 轴方向 (0 or "index", 1 or "columns")
        **kwargs
    )
# 在某个索引值之前和之后截断 Series 或 DataFrame
DataFrame.truncate(
        before=None,  # 前
        after=None,  # 后
        axis=None,  # 轴方向 (0 or "index", 1 or "columns")
        copy=True
    )
```

## 缺失数据处理
```python

```