


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

# 2. 一般功能能

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