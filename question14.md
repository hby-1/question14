# 判断两个事件是否存在冲突

给你两个字符串数组 `event1` 和 `event2` ，表示发生在同一天的两个闭区间时间段事件，其中：

- event1 = [startTime1, endTime1] 且
- event2 = [startTime2, endTime2]
事件的时间为有效的 24 小时制且按 HH:MM 格式给出。

当两个事件存在某个非空的交集时（即，某些时刻是两个事件都包含的），则认为出现 **冲突** 。

如果两个事件之间存在冲突，返回 `true` ；否则，返回 `false` 。

## 示例 1：
>### 输入：
>event1 = ["01:15","02:00"], event2 = ["02:00","03:00"]
>### 输出：
>true
>### 解释：
>两个事件在 2:00 出现交集。

## 示例 2：
>### 输入：
>event1 = ["01:00","02:00"], event2 = ["01:20","03:00"]
>### 输出：
>true
>### 解释：
>两个事件的交集从 01:20 开始，到 02:00 结束。

## 示例 3：
>### 输入：
>event1 = ["10:00","11:00"], event2 = ["14:00","15:00"]
>### 输出：
>false
>### 解释：
>两个事件没有交集。

## 代码：
1.

    public class Solution {
        public bool HaveConflict(string[] event1, string[] event2) {
            if(TimeSpan.Parse(event2[0])<=TimeSpan.Parse(event1[1])&&TimeSpan.Parse(event1[1])<=TimeSpan.Parse(event2[1])){
                return true;
            }
            if(TimeSpan.Parse(event1[0])<=TimeSpan.Parse(event2[1])&&TimeSpan.Parse(event2[1])<=TimeSpan.Parse(event1[1])){
                return true;
            }
            else{
                return false;
            }
        }
    }
2.

    public class Solution {
        public bool HaveConflict(string[] event1, string[] event2) {
            // 将字符串时间转换为 TimeSpan 对象
            TimeSpan startTime1 = TimeSpan.Parse(event1[0]);
            TimeSpan endTime1 = TimeSpan.Parse(event1[1]);
            TimeSpan startTime2 = TimeSpan.Parse(event2[0]);
            TimeSpan endTime2 = TimeSpan.Parse(event2[1]);
            
            // 判断是否存在时间重叠
            return startTime1 <= endTime2 && startTime2 <= endTime1;
        }
    }
3.

    public class Solution {
        public bool HaveConflict(string[] event1, string[] event2) {
            return event1[1].CompareTo(event2[0]) >= 0 && event2[1].CompareTo(event1[0]) >= 0;
        }
    }


