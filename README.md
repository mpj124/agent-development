---
name: date_and_math_calculator
domain: common
description: 执行 Python 代码来解决数学和日期计算问题。可用的库和函数：
---

# date_and_math_calculator

执行 Python 代码来解决数学和日期计算问题。可用的库和函数：
1. 数学库：math 模块 (sqrt, sin, cos, pow, log, exp, ceil, floor 等)
2. 日期时间：datetime, timedelta, date
3. 农历转换：Lunar, Solar, Converter (lunarcalendar库)
   - Lunar(year, month, day, isleap=False) 创建农历日期
   - Converter.Lunar2Solar(lunar) 农历转公历
   - Converter.Solar2Lunar(solar) 公历转农历
4. 必须使用 f-string 或者 format 来格式化输出

代码示例：
示例1 - 查询农历节日日期：
```python
# 查询 2025年春节 (农历正月初一)
lunar = Lunar(2025, 1, 1, isleap=False)
solar = Converter.Lunar2Solar(lunar)
result = f"{solar.year}年{solar.month}月{solar.day}日"
```
示例2 - 计算相对日期：
```python
# 春节前5天
lunar = Lunar(2026, 1, 1, isleap=False)
solar = Converter.Lunar2Solar(lunar)
spring_date = datetime(solar.year, solar.month, solar.day)
target_date = spring_date - timedelta(days=5)
# 注意: 必须使用 f-string 格式化, 不能使用 strftime
result = f"{target_date.year}-{target_date.month:02d}-{target_date.day:02d}"
```
示例3 - 日期间隔计算：
```python
# 今天到春节还有多少天
lunar = Lunar(2026, 1, 1, isleap=False)
solar = Converter.Lunar2Solar(lunar)
spring = datetime(solar.year, solar.month, solar.day)
today = datetime.now()
days_left = (spring - today).days
result = f"还有 {days_left} 天"
```
示例4 - 数学计算：
```python
# 数学计算: 计算 2 的 10 次方加上 144 的平方根
val1 = math.pow(2, 10)
val2 = math.sqrt(144)
result = f"2的10次方是{val1}, 144的平方根是{val2}, 总和是{val1 + val2}"
```

常用农历节日对应：
- 春节：正月初一 (1, 1)
- 元宵节：正月十五 (1, 15)
- 端午节：五月初五 (5, 5)
- 七夕：七月初七 (7, 7)
- 中秋节：八月十五 (8, 15)
- 重阳节：九月初九 (9, 9)
- 除夕：春节前一天

重要规则：
1. 代码必须将最终结果赋值给 result 变量
2. 不能使用 import 语句（所有库已预导入）
3. 禁止文件操作、网络请求、系统调用
4. 代码执行有超时限制

## 参数

| 参数名 | 类型 | 必填 | 说明 | 示例 |
|--------|------|------|------|------|
| code | string | ✅ | 要执行的 Python 代码。必须将最终结果赋值给 result 变量。 | - |
| description | string | ❌ | 代码的用途说明，用于日志记录和调试。例如：'计算2025年春节日期'、'查询春节前5天' | - |

## 输出参数

```json
{
  "type": "object",
  "properties": {
    "code": {
      "type": "string",
      "description": "要执行的 Python 代码。必须将最终结果赋值给 result 变量。"
    },
    "description": {
      "type": "string",
      "description": "代码的用途说明，用于日志记录和调试。例如：'计算2025年春节日期'、'查询春节前5天'"
    }
  },
  "required": [
    "code"
  ]
}
```
