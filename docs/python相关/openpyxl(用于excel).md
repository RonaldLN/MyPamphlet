## 1

>   [2023数模国赛](https://ronaldln.github.io/MyPamphlet-Blog/2023/09/08/2023/)

*读取*和*写入*的函数

```python
import openpyxl


# 定义一个函数，从 Excel 文件中获取数据并存储到列表中
def get_data_from_excel(file_name, sheet_name):
    # 创建一个空列表来存储数据
    data_list = []
    # 打开 Excel 文件
    wb = openpyxl.load_workbook(file_name)
    # 获取工作表
    sheet = wb[sheet_name]
    # 获取最大行数
    max_row = sheet.max_row
    # 获取最大列数
    max_column = sheet.max_column
    # 使用循环从 Excel 文件中获取数据
    for i in range(2, max_row + 1):
        # 创建一个空列表来存储每行的数据
        sub_list = []
        for j in range(1, max_column + 1):
            # 获取每个单元格的数据
            cell = sheet.cell(row=i, column=j)
            # 将数据添加到子列表中
            sub_list.append(cell.value)
        # 将子列表添加到数据列表中
        data_list.append(sub_list)
    # 返回数据列表
    return data_list


# 定义一个函数，将数据写入 Excel 文件中
def write_data_to_excel(file_name, sheet_name, data_list):
    # 打开 Excel 文件
    wb = openpyxl.load_workbook(file_name)
    # 如果工作表不存在，则创建它
    if sheet_name not in wb.sheetnames:
        wb.create_sheet(sheet_name)
    # 获取工作表
    sheet = wb[sheet_name]
    # 根据数据的大小获取最大行数和列数
    max_row = len(data_list)
    max_column = len(data_list[0])
    # 使用循环将数据写入 Excel 文件中
    for i in range(2, max_row + 2):
        for j in range(1, max_column + 1):
            # 获取每个单元格的数据
            cell = sheet.cell(row=i, column=j)
            # 将数据写入单元格
            cell.value = data_list[i - 2][j - 1]
    # 保存 Excel 文件
    wb.save(file_name)
```

-   注意：**写入的函数需要目标文件已经创建好/已经存在**
-   该写入函数将list列表写入excel表格时，会空出第一行(可以用于填写栏目名称)

---

??? example "chat log"

    **user**:
    
    ```python
    import openpyxl


    # define a function to get the data from an Excel file to a list
    def get_data(file_name, sheet_name):
        # create an empty list to store the data
        data_list = []
        # open the Excel file
        wb = openpyxl.load_workbook(file_name)
        # get the sheet
        sheet = wb[sheet_name]
        # get the max row
        max_row = sheet.max_row
        # get the max column
        max_column = sheet.max_column
        # use a for loop to get the data from the Excel file
        for i in range(2, max_row + 1):
            # create an empty list to store the data of each row
            sub_list = []
            for j in range(1, max_column + 1):
                # get the data of each cell
                cell = sheet.cell(row=i, column=j)
                # add the data to the sub list
                sub_list.append(cell.value)
            # add the sub list to the data list
            data_list.append(sub_list)
        # return the data list
        return data_list


    data = get_data("data.xlsx", "Sheet1")
    # print(data)
    new_data = []
    for line in data:
        if line[1] == 'A':
            line[2] /= 0.6
            line[3] /= 0.6
        elif line[1] == 'B':
            line[2] /= 0.66
            line[3] /= 0.66
        else:
            line[2] /= 0.72
            line[3] /= 0.72
        new_data += [line]
    
    # print(new_data)


    # define a function to write the data to an Excel file
    def write_data(file_name, sheet_name, data_list):
        # open the Excel file
        wb = openpyxl.load_workbook(file_name)
        # get the sheet
        sheet = wb[sheet_name]
        # get the max row
        max_row = sheet.max_row
        # get the max column
        max_column = sheet.max_column
        # use a for loop to write the data to the Excel file
        for i in range(2, max_row + 1):
            for j in range(1, max_column + 1):
                # get the data of each cell
                cell = sheet.cell(row=i, column=j)
                # write the data to the cell
                cell.value = data_list[i - 2][j - 1]
        # save the Excel file
        wb.save(file_name)


    write_data("data.xlsx", "Sheet2", new_data)
    ```
    
    My code did not successfully write the data to the Excel file. Can you help me see what the error is and how to modify it?
    
    **chatgpt**:
    
    Based on the code you provided, there are a couple of issues that might be causing the problem you are encountering when trying to write data to an Excel file:
    
    1.  The "Sheet2" sheet does not exist in the Excel file.
    
    If the sheet you are trying to write to does not exist in the Excel file, you will need to create it first before you can write data to it. You can do this using the `create_sheet()` method of the workbook object. For example:
    
    ```python
    wb.create_sheet("Sheet2")
    ```
    
    2.  The range of cells to write to is incorrect.
    
    In the `write_data()` function, the range of cells to write to is determined based on the maximum number of rows and columns in the sheet. However, if the size of the data you are trying to write is smaller than the size of the sheet, you will end up overwriting some cells with empty values. To avoid this, you should use the actual size of the data to determine the range of cells to write to. You can do this by using the `len()` function to get the number of rows in the data list. For example:
    
    ```python
    max_row = len(data_list)
    max_column = len(data_list[0])
    ```
    
    Here's the modified code with these changes:
    
    ```python
    import openpyxl


    # define a function to get the data from an Excel file to a list
    def get_data(file_name, sheet_name):
        # create an empty list to store the data
        data_list = []
        # open the Excel file
        wb = openpyxl.load_workbook(file_name)
        # get the sheet
        sheet = wb[sheet_name]
        # get the max row
        max_row = sheet.max_row
        # get the max column
        max_column = sheet.max_column
        # use a for loop to get the data from the Excel file
        for i in range(2, max_row + 1):
            # create an empty list to store the data of each row
            sub_list = []
            for j in range(1, max_column + 1):
                # get the data of each cell
                cell = sheet.cell(row=i, column=j)
                # add the data to the sub list
                sub_list.append(cell.value)
            # add the sub list to the data list
            data_list.append(sub_list)
        # return the data list
        return data_list


    data = get_data("data.xlsx", "Sheet1")
    # print(data)
    new_data = []
    for line in data:
        if line[1] == 'A':
            line[2] /= 0.6
            line[3] /= 0.6
        elif line[1] == 'B':
            line[2] /= 0.66
            line[3] /= 0.66
        else:
            line[2] /= 0.72
            line[3] /= 0.72
        new_data += [line]
    
    # print(new_data)


    # define a function to write the data to an Excel file
    def write_data(file_name, sheet_name, data_list):
        # open the Excel file
        wb = openpyxl.load_workbook(file_name)
        # create the sheet if it doesn't exist
        if sheet_name not in wb.sheetnames:
            wb.create_sheet(sheet_name)
        # get the sheet
        sheet = wb[sheet_name]
        # get the max row and column based on the size of the data
        max_row = len(data_list)
        max_column = len(data_list[0])
        # use a for loop to write the data to the Excel file
        for i in range(2, max_row + 2):
            for j in range(1, max_column + 1):
                # get the data of each cell
                cell = sheet.cell(row=i, column=j)
                # write the data to the cell
                cell.value = data_list[i - 2][j - 1]
        # save the Excel file
        wb.save(file_name)


    write_data("data.xlsx", "Sheet2", new_data)
    ```
    
    With these changes, the code should now write the data to the "Sheet2" sheet in the "data.xlsx" file.


    **user**:
    
    你能用中文再输出一遍吗？
    
    **chatgpt**:
    
    当你尝试向 Excel 文件写入数据时，代码可能出现一些问题。根据你提供的代码，可能会出现以下问题：
    
    1.  Excel 文件中不存在 "Sheet2" 工作表。
    
    如果你尝试写入的工作表在 Excel 文件中不存在，你需要先创建它才能向其写入数据。你可以使用工作簿对象的 `create_sheet()` 方法来创建工作表。例如：
    
    ```python
    wb.create_sheet("Sheet2")
    ```
    
    2.  要写入的单元格范围不正确。
    
    在 `write_data()` 函数中，要写入的单元格范围是基于工作表的最大行数和列数来确定的。但是，如果你要写入的数据大小小于工作表的大小，你将会覆盖一些单元格，使它们的值为空。为了避免这种情况，你应该使用实际数据的大小来确定要写入的单元格范围。你可以使用 `len()` 函数获取数据列表中的行数。例如：
    
    ```python
    max_row = len(data_list)
    max_column = len(data_list[0])
    ```
    
    以下是修改后的代码，其中包含这些更改：
    
    ```python
    import openpyxl


    # 定义一个函数，从 Excel 文件中获取数据并存储到列表中
    def get_data(file_name, sheet_name):
        # 创建一个空列表来存储数据
        data_list = []
        # 打开 Excel 文件
        wb = openpyxl.load_workbook(file_name)
        # 获取工作表
        sheet = wb[sheet_name]
        # 获取最大行数
        max_row = sheet.max_row
        # 获取最大列数
        max_column = sheet.max_column
        # 使用循环从 Excel 文件中获取数据
        for i in range(2, max_row + 1):
            # 创建一个空列表来存储每行的数据
            sub_list = []
            for j in range(1, max_column + 1):
                # 获取每个单元格的数据
                cell = sheet.cell(row=i, column=j)
                # 将数据添加到子列表中
                sub_list.append(cell.value)
            # 将子列表添加到数据列表中
            data_list.append(sub_list)
        # 返回数据列表
        return data_list


    data = get_data("data.xlsx", "Sheet1")
    # print(data)
    new_data = []
    for line in data:
        if line[1] == 'A':
            line[2] /= 0.6
            line[3] /= 0.6
        elif line[1] == 'B':
            line[2] /= 0.66
            line[3] /= 0.66
        else:
            line[2] /= 0.72
            line[3] /= 0.72
        new_data += [line]
    
    # print(new_data)


    # 定义一个函数，将数据写入 Excel 文件中
    def write_data(file_name, sheet_name, data_list):
        # 打开 Excel 文件
        wb = openpyxl.load_workbook(file_name)
        # 如果工作表不存在，则创建它
        if sheet_name not in wb.sheetnames:
            wb.create_sheet(sheet_name)
        # 获取工作表
        sheet = wb[sheet_name]
        # 根据数据的大小获取最大行数和列数
        max_row = len(data_list)
        max_column = len(data_list[0])
        # 使用循环将数据写入 Excel 文件中
        for i in range(2, max_row + 2):
            for j in range(1, max_column + 1):
                # 获取每个单元格的数据
                cell = sheet.cell(row=i, column=j)
                # 将数据写入单元格
                cell.value = data_list[i - 2][j - 1]
        # 保存 Excel 文件
        wb.save(file_name)


    write_data("data.xlsx", "Sheet2", new_data)
    ```
    
    经过这些更改，代码现在应该能够将数据写入到 "data.xlsx" 文件中的 "Sheet2" 工作表中。
