#form表单相关元素

## Type类型

### 数据

| 类型      | 说明      |
| ------- | ------- |
| integer | 整数数字输入框 |
| float   | 浮点数字输入框 |
| currency| 货币输入框 |
| password| 密码输入框 |
| percent | 百分比输入框 |
| string  | 字符串输入框 |

### 日期

| 类型            | 说明           |
| ------------- | ------------ |
| u-year        | 年份控件         |
| u-month       | 月份输入框        |
| u-yearmonth   | 年份月份控件       |
| u-monthdate   | 月日控件       |
| u-time        | 时间控件         |
| u-clockpicker | 时间控件，显示为钟表形式 |
| u-date        | 日期输入框        |
| u-datetime   | 日期时间输入框      |

* `u-date` , `u-datetime` 表示元素为日期时间输入框

  > 时间日期有`format`属性，type为`u-date`时`format`默认为“YYYY-MM-DD”，type为`u-datetime`时`format`默认为“YYYY-MM-DD HH:mm:ss”



### 文本

| 类型       | 说明    |
| -------- | ----- |
| textarea | 文本域   |
| u-text   | 文本输入框 |



### 选择下拉

| 类型          | 说明   |
| ----------- | ---- |
| u-combobox | 下拉框  |
| u-checkbox | 复选框  |
| u-radio    | 单选   |
| u-switch   | 选择开关  |


# 非表单元素

## Type类型

| 类型  | 说明   |
| ----  | ---- |
| grid | grid表格  |
| u-progress | 进度条  |
| pagination | 分页  |
| tree | 树控件  |