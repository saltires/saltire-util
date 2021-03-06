# 日期模块

## `between` <Badge text="0.0.1+"/>

``` javascript
between: (
    date: potentialDate,
    start: potentialDate,
    end: potentialDate
) => boolean;
```

#### 功能描述

`日期区间判断`：判断指定日期是否在指定的开始日期和结束日期之间

#### 参数

- `date(string | number | Date)`：必须，指定日期
- `start(string | number | Date)`：必须，开始日期
- `end(string | number | Date)`：必须，结束日期

#### 返回

`(Boolean)`：true 表示指定日期在指定的区间之内，相反则不在

#### 示例

``` javascript
const { date } = require('../lib/date')

test('测试 between', () => {
    const date1 = new Date('2020-05-02')
    const start = new Date('2020-01-02')
    const end = new Date('2020-10-02')

    expect(date.between('2020-05-02', '2020-01-02', '2020-10-02')).toBe(true)
    expect(date.between('2019-05-02', '2020-01-02', '2020-10-02')).toBe(false)
    expect(date.between(date1, start, end)).toBe(true)
    expect(date.between(date1, end, start)).toBe(false)
    expect(date.between(+date1, +start, +end)).toBe(true)
    expect(date.between(+date1, +end, +start)).toBe(false)
})

// all passed
```

<br>
<br>

## `renderDate` <Badge text="0.0.1+"/>

``` javascript
renderDate: (date: potentialDate, format?: string) => string;
```

#### 功能描述

`日期格式化`：日期格式化工具函数

#### 参数

- `date(string | number | Date)`：必须，需要格式化的日期
- `format(string)`：必须，格式化规则

#### 返回

`str(String)`：格式化后的日期字符串

#### 示例

``` javascript
const { date } = require('../lib/date')

test('测试 renderDate', () => {
    const format = ['yyyy-MM-dd:HH:mm:ss','yyyy-MM-dd', 'yyyy年MM月dd日HH时mm分', 'yyyy年MM月dd日HH时mm分ss秒']
    const date1 = new Date(1615342454266)

    for (let [key, value] of Object.entries(format)){
        switch (key) {
            case '0':
                expect(date.renderDate(date1, value)).toBe('2021-03-10:10:14:14')
                break;
            case '1':
                expect(date.renderDate(date1, value)).toBe('2021-03-10')
                break;
            case '2':
                expect(date.renderDate(date1, value)).toBe('2021年03月10日10时14分')
                break;
            case '3':
                expect(date.renderDate(date1, value)).toBe('2021年03月10日10时14分14秒')
                break;
        }
        
    }
})

// all passed
```

<br>
<br>

## `isEqual` <Badge text="0.0.1+"/>

``` javascript
isEqual: (date1: potentialDate, date2: potentialDate) => boolean;
```

#### 功能描述

`判断日期是否相等`：判断两个日期是否相等

#### 参数

- `date1(string | number | Date)`：必须，日期 1
- `date2(string | number | Date)`：必须，日期 2

#### 返回

`bol(Boolean)`：日期相等返回 true，否则返回 false

#### 示例

``` javascript
const { date } = require('../lib/date')

test('测试 isEqual', () => {
    const date1 = new Date('2020-01-01')
    const date2 = new Date('2020-01-01')
    const date3 = new Date('2021-10-01')

    expect(date.isEqual(date1, date2)).toBe(true)
    expect(date.isEqual(date1, date3)).toBe(false)
    expect(date.isEqual(date2, date3)).toBe(false)
})

// all passed
```

<br>
<br>

## `isLeapYear` <Badge text="0.0.1+"/>

``` javascript
isLeapYear: (date: potentialDate) => boolean;
```

#### 功能描述

`是否是闰年`：判断指定日期是否是闰年

#### 参数

- `date(string | number | Date)`：必须，待判断的日期

#### 返回

`bol(Boolean)`：是闰年返回 true，否则返回 false

#### 示例

``` javascript
const { date } = require('../lib/date')

test('测试 isLeapYear', () => {
    const date1 = new Date('2021-01-01')
    const date2 = new Date('2020-01-01')
    const date3 = new Date('2019-01-01')
    const date4 = new Date('2018-01-01')

    expect(date.isLeapYear(date1)).toBe(false)
    expect(date.isLeapYear(date2)).toBe(true)
    expect(date.isLeapYear(date3)).toBe(false)
    expect(date.isLeapYear(date4)).toBe(false)
})

// all passed
```

<br>
<br>

## `getFirstDayOfMonth` <Badge text="0.0.1+"/>

``` javascript
getFirstDayOfMonth: (date: potentialDate) => number;
```

#### 功能描述

`判断是周几`：返回指定年月的第一天是星期几，返回值是1-7的数字

#### 参数

- `date(string | number | Date)`：必须，待判断的日期

#### 返回

`number(number)`：返回值是1-7的数字，分别代表周一到周日

#### 示例

``` javascript
const { date } = require('../lib/date')

test('测试 getFirstDayOfMonth', () => {
    // 2021 的 3 月的第一天是星期一
    const date1 = new Date('2021-03-10')
    // 2021 的 2 月的第一天是星期一
    const date2 = new Date('2021-02-10')
    // 2021 的 1 月的第一天是星期五
    const date3 = new Date('2021-01-10')
    // 2020 的 12 月的第一天是星期二
    const date4 = new Date('2020-12-10')

    expect(date.getFirstDayOfMonth(date1)).toBe(1)
    expect(date.getFirstDayOfMonth(date2)).toBe(1)
    expect(date.getFirstDayOfMonth(date3)).toBe(5)
    expect(date.getFirstDayOfMonth(date4)).toBe(2)
})

// all passed
```

<br>
<br>

## `getLastDayOfMonth` <Badge text="0.0.1+"/>

``` javascript
getLastDayOfMonth: (date: potentialDate) => number;
```

#### 功能描述

`判断是周几`：返回指定月份的最后一天是星期几，返回值是1-7的数字

#### 参数

- `date(string | number | Date)`：必须，待判断的日期

#### 返回

`number(number)`：返回值是1-7的数字，分别代表周一到周日

#### 示例

``` javascript
const { date } = require('../lib/date')

test('测试 getLastDayOfMonth', () => {
    // 2021 的 3 月的第一天是星期一
    const date1 = new Date('2021-03-10')
    // 2021 的 2 月的第一天是星期一
    const date2 = new Date('2021-02-10')
    // 2021 的 1 月的第一天是星期五
    const date3 = new Date('2021-01-10')
    // 2020 的 12 月的第一天是星期二
    const date4 = new Date('2020-12-10')

    expect(date.getLastDayOfMonth(date1)).toBe(3)
    expect(date.getLastDayOfMonth(date2)).toBe(7)
    expect(date.getLastDayOfMonth(date3)).toBe(7)
    expect(date.getLastDayOfMonth(date4)).toBe(4)
})

// all passed
```

<br>
<br>

## `getFirstDateOfMonth` <Badge text="0.0.1+"/>

``` javascript
getFirstDateOfMonth: (date: potentialDate) => string;
```

#### 功能描述

`获取某月第一天日期`：返回指定年月第一天的日期

#### 参数

- `date(string | number | Date)`：必须，指定的年月

#### 返回

`str(String)`：返回值是日期字符串

#### 示例

``` javascript
const { date } = require('../lib/date')

test('测试 getFirstDateOfMonth', () => {
    // 2021 的 3 月的第一天是星期一
    const date1 = new Date('2021-03-10')
    // 2021 的 2 月的第一天是星期一
    const date2 = new Date('2021-02-10')
    // 2021 的 1 月的第一天是星期五
    const date3 = new Date('2021-01-10')
    // 2020 的 12 月的第一天是星期二
    const date4 = new Date('2020-12-10')

    expect(date.getFirstDateOfMonth(date1)).toBe('2021-03-01')
    expect(date.getFirstDateOfMonth(date2)).toBe('2021-02-01')
    expect(date.getFirstDateOfMonth(date3)).toBe('2021-01-01')
    expect(date.getFirstDateOfMonth(date4)).toBe('2020-12-01')
})

// all passed
```

<br>
<br>

## `getLastDateOfMonth` <Badge text="0.0.1+"/>

``` javascript
getLastDateOfMonth: (date: potentialDate) => string;
```

#### 功能描述

`获取某月最后一天日期`：返回指定年月最后一天的日期

#### 参数

- `date(string | number | Date)`：必须，指定的年月

#### 返回

`str(String)`：返回值是日期字符串

#### 示例

``` javascript
const { date } = require('../lib/date')

test('测试 getFirstDateOfMonth', () => {
    // 2021 的 3 月的第一天是星期一
    const date1 = new Date('2021-03-10')
    // 2021 的 2 月的第一天是星期一
    const date2 = new Date('2021-02-10')
    // 2021 的 1 月的第一天是星期五
    const date3 = new Date('2021-01-10')
    // 2020 的 12 月的第一天是星期二
    const date4 = new Date('2020-12-10')

    expect(date.getLastDateOfMonth(date1)).toBe('2021-03-31')
    expect(date.getLastDateOfMonth(date2)).toBe('2021-02-28')
    expect(date.getLastDateOfMonth(date3)).toBe('2021-01-31')
    expect(date.getLastDateOfMonth(date4)).toBe('2020-12-31')
})

// all passed
```

<br>
<br>

## `getDaysInMonth` <Badge text="0.0.1+"/>

``` javascript
getDaysInMonth: (date: potentialDate) => number;
```

#### 功能描述

`获取指定月份的天数`：获取指定月份的天数

#### 参数

- `date(string | number | Date)`：必须，指定的年月

#### 返回

`days(number)`：返回值是数字

#### 示例

``` javascript
const { date } = require('../lib/date')

test('测试 getDaysInMonth', () => {
    // 2021 的 3 月的第一天是星期一
    const date1 = new Date('2021-03-10')
    // 2021 的 2 月的第一天是星期一
    const date2 = new Date('2021-02-10')
    // 2021 的 1 月的第一天是星期五
    const date3 = new Date('2021-01-10')
    // 2020 的 12 月的第一天是星期二
    const date4 = new Date('2020-12-10')

    expect(date.getDaysInMonth(date1)).toBe(31)
    expect(date.getDaysInMonth(date2)).toBe(28)
    expect(date.getDaysInMonth(date3)).toBe(31)
    expect(date.getDaysInMonth(date4)).toBe(31)
})

// all passed
```

<br>
<br>

## `addDays` <Badge text="0.0.1+"/>

``` javascript
addDays: (date: potentialDate, days: number) => Date;
```

#### 功能描述

`给指定日期增加指定天数`：给指定日期增加指定天数

#### 参数

- `date(string | number | Date)`：必须，指定的日期
- `day(number)`：必须，要增加的天数

#### 返回

`date(Date)`：返回值是 Javascript 日期对象

#### 示例

``` javascript
const { date } = require('../lib/date')

test('测试 addDays', () => {
    // 2021 的 3 月的第一天是星期一
    const date1 = new Date('2021-03-10')
    // 2021 的 2 月的第一天是星期一
    const date2 = new Date('2021-02-10')
    // 2021 的 1 月的第一天是星期五
    const date3 = new Date('2021-01-10')
    // 2020 的 12 月的第一天是星期二
    const date4 = new Date('2020-12-10')

    expect(date.renderDate(date.addDays(date1, 1))).toBe('2021-03-11')
    expect(date.renderDate(date.addDays(date2, 2))).toBe('2021-02-12')
    expect(date.renderDate(date.addDays(date3, 3))).toBe('2021-01-13')
    expect(date.renderDate(date.addDays(date4, 4))).toBe('2020-12-14')
})

// all passed
```

<br>
<br>

## `addHours` <Badge text="0.0.1+"/>

``` javascript
addHours: (date: potentialDate, hours: number) => Date;
```

#### 功能描述

`给指定日期增加指定小时`：给指定日期增加指定小时

#### 参数

- `date(string | number | Date)`：必须，指定的日期
- `hour(number)`：必须，要增加的小时

#### 返回

`date(Date)`：返回值是 Javascript 日期对象

#### 示例

``` javascript
const { date } = require('../lib/date')

test('测试 addHours', () => {
    // 2021 的 3 月的第一天是星期一
    const date1 = new Date('2021-03-10:08:00:00')
    // 2021 的 2 月的第一天是星期一
    const date2 = new Date('2021-02-10:08:00:00')
    // 2021 的 1 月的第一天是星期五
    const date3 = new Date('2021-01-10:08:00:00')
    // 2020 的 12 月的第一天是星期二
    const date4 = new Date('2020-12-10:08:00:00')

    expect(date.renderDate(date.addHours(date1, 1), 'yyyy-MM-dd:HH:mm:ss')).toBe('2021-03-10:09:00:00')
    expect(date.renderDate(date.addHours(date2, 2), 'yyyy-MM-dd:HH:mm:ss')).toBe('2021-02-10:10:00:00')
    expect(date.renderDate(date.addHours(date3, 3), 'yyyy-MM-dd:HH:mm:ss')).toBe('2021-01-10:11:00:00')
    expect(date.renderDate(date.addHours(date4, 4), 'yyyy-MM-dd:HH:mm:ss')).toBe('2020-12-10:12:00:00')
})

// all passed
```

<br>
<br>

## `timeStartChange` <Badge text="0.0.1+"/>

``` javascript
timeStartChange: (date: potentialDate) => number;
```

#### 功能描述

`日期转时间戳`：将时间转为时间戳，按当天最初一刻

#### 参数

- `date(string | number | Date)`：必须，指定的日期

#### 返回

`date(number)`：返回值是时间戳

#### 示例

``` javascript
const { date } = require('../lib/date')

test('测试 timeStartChange', () => {
    // 2021 的 3 月的第一天是星期一
    const date1 = new Date('2021-03-10')
    // 2021 的 2 月的第一天是星期一
    const date2 = new Date('2021-02-10')
    // 2021 的 1 月的第一天是星期五
    const date3 = new Date('2021-01-10')
    // 2020 的 12 月的第一天是星期二
    const date4 = new Date('2020-12-10')

    expect(date.timeStartChange(date1)).toBe(1615305600000)
    expect(date.timeStartChange(date2)).toBe(1612886400000)
    expect(date.timeStartChange(date3)).toBe(1610208000000)
    expect(date.timeStartChange(date4)).toBe(1607529600000)
})

// all passed
```

<br>
<br>

## `timeEndChange` <Badge text="0.0.1+"/>

``` javascript
timeEndChange: (date: potentialDate) => number;
```

#### 功能描述

`日期转时间戳`：将时间转为时间戳，按当天最后一刻

#### 参数

- `date(string | number | Date)`：必须，指定的日期

#### 返回

`date(number)`：返回值是时间戳

#### 示例

``` javascript
const { date } = require('../lib/date')

test('测试 timeEndChange', () => {
    // 2021 的 3 月的第一天是星期一
    const date1 = new Date('2021-03-10')
    // 2021 的 2 月的第一天是星期一
    const date2 = new Date('2021-02-10')
    // 2021 的 1 月的第一天是星期五
    const date3 = new Date('2021-01-10')
    // 2020 的 12 月的第一天是星期二
    const date4 = new Date('2020-12-10')

    expect(date.timeEndChange(date1)).toBe(1615391999000)
    expect(date.timeEndChange(date2)).toBe(1612972799000)
    expect(date.timeEndChange(date3)).toBe(1610294399000)
    expect(date.timeEndChange(date4)).toBe(1607615999000)
})

// all passed
```

<br>
<br>

## `timeDifference` <Badge text="0.0.1+"/>

``` javascript
timeDifference: (time1: number, time2: number) => dateObject;
```

#### 功能描述

`日期转时间戳`：获取时间差，提供两个时间戳，返回一个对象，为负数表示当前 time1 比 time2 小

#### 参数

- `time1(number)`：必须，第一个时间的时间戳
- `time2(number)`：必须，第二个时间的时间戳

#### 返回

`dateObject(dateObject)`：返回值是一个对象，内部详细的描述了相差的天数、小时、分钟等

#### 示例

``` javascript
const { date } = require('../lib/date')

test('测试 timeDifference', () => {
    // 2021 的 3 月的第一天是星期一
    const date1 = new Date('2021-03-10')
    // 2021 的 2 月的第一天是星期一
    const date2 = new Date('2021-03-09')

    expect(date.timeDifference(date1, date2)).toEqual({
        day: -1,
        hour: 0,
        min: 0,
        ms: 0
    })
})

// all passed
```