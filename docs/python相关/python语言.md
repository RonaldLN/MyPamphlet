!!! info

    此处用于记录我自己发现的python中的(我之前不知道的)操作

## 1

>   2023数模国赛

**==在字典中直接查询、取出的是 key 的值==**

**1**

`in` 语句可以判断 某个 key 是否在某个字典中，如

```python
# 从附录2的Excel表格中读取数据
datas2 = get_data("2.xlsx", "Sheet1")
# 创建一个字典来存储销量数据，字典的键是产品编号，值是包含销售季度数据的嵌套字典
xiaoliang = {}
# 遍历附录2中的数据
for data in datas2:
    # 如果产品编号不在字典中，添加一个新的键值对
    if data[2] not in xiaoliang:
        # 销售数据字典的键是年份和季度的组合，初始值为0
        xiaoliang[data[2]] = {y * 100 + s: 0 for y in range(2020, 2024) for s in range(1, 5)}
    # 更新销售数据字典，根据销售日期获取季度并将销售数量累加到相应的季度
    xiaoliang[data[2]][get_season(data[0])] += data[3]
```

其中

```python
    if data[2] not in xiaoliang:
        ...
```

能判断字典xiaoliang是否已经存在为 `data[2]` 的键(没有可以进行初始化等操作)

**2**

>   2023数模国赛

`for` 语句(循环以及列表推导式)直接用于字典取出的是 key，

```python
for xl in xiaoliang:
    new_xl = [round(xiaoliang[xl][x], 3) for x in xiaoliang[xl]]
    xiaoliang[xl] = new_xl
```

如果需要取出 value 则可以使用字典的 `.item()` (取出key和value) 或 `.values()` (只取出value) 方法：

```python
# 定义一个函数，将dict转换成list
def dict_to_list(dict1):
    list1 = []
    for key, value in dict1.items():
        list1.append([key, value])
    return list1
```

```python
for value in xxx.values():
    ...
```

## 3

>   2023数模国赛

字典的 `.values()` 方法，返回的是一个 dict_values 类型，如果需要的是列表，则需要类型转换：

```bash
>>> d = {"key": 0}
>>> d.values()
dict_values([0])
>>> list(d.values())
[0]
```

## 4

>   2023数模国赛

**字典不能切片**

## 5

>   2023数模国赛

!!! note

    json文件读取速度很快，我认为很适合用于处理数据

读取和写入json文件的函数

```python
import json


# 定义一个函数，将dict存到指定的json文件中
def write_data(file_name, data):
    # 打开json文件
    with open(file_name, "w", encoding="utf-8") as f:
        # 将数据写入json文件中
        json.dump(data, f, ensure_ascii=False, indent=4)


# 定义一个函数，从json文件中读取数据
def read_data(file_name):
    # 打开json文件
    with open(file_name, "r", encoding="utf-8") as f:
        # 读取json文件中的数据
        data = json.load(f)
        # 返回数据
        return data
```

-   写入函数如果目标文件不存在，会自动新建一个对应的文件
-   写入函数需要传入一个字典，(如果想存储列表类型的数据，可以在列表外套一个只含一个键的字典)

## 6

>   2023数模国赛

对小数四舍五入 使用 `round()` 函数，如

```python
# 将结果数据的小数位数保留三位
for _, value in data_res.items():
    for i in range(12):
        value[i] = round(value[i], 3)
```

第一个参数时要*舍入*的值，第二个参数是要保留的小数位数

## 7

>   2023数模国赛

datetime类型

-   datetime可以直接获取 年、月、日 等的数据

    ```python
    # 定义一个函数，传入datetime，判断在哪一年的哪个季度中
    def get_season(date):
        season = 0
        if date.month in [1, 2, 3]:
            season = 1
        elif date.month in [4, 5, 6]:
            season = 2
        elif date.month in [7, 8, 9]:
            season = 3
        elif date.month in [10, 11, 12]:
            season = 4
        return int(date.year * 100 + season)
    ```

-   datetime可以类型转换成str，会转成形如 `"2023-09-11 18:40:22.834683"` 的字符串

    ```python
    >>> import datetime
    >>> now = datetime.datetime.now()
    >>> now
    datetime.datetime(2023, 9, 11, 18, 40, 22, 834683)
    >>> str(now)
    '2023-09-11 18:40:22.834683'
    ```

## 8

>   2023数模国赛

将列表写入csv文件的函数

```python
# 定义一个函数，将list存入csv文件
def write_data_to_csv(file_name, data_list):
    # 打开csv文件
    with open(file_name, "w", encoding="gbk", newline="") as f:
        # 创建一个csv写入器
        writer = csv.writer(f)
        # 将数据写入csv文件中
        writer.writerows(data_list)
```

`encoding` 参数是编码格式，选择 `"gbk"` excel能正常打开，选择 `"utf-8"` excel好像会显示乱码
