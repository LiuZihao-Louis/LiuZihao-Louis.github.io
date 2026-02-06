# 单调栈

- 单调**递增**栈 -> 得到当前右面第一个比他***大***的元素
  - ​     30    -> 10 20   则30为10右面第一个比他大的元素；20为左边第一个比他大的元素（有待确认，应该是
- 单调**递减**栈 -> 得到当前右面第一个比他***小***的元素

[leetcode-42 接雨水](https://leetcode.cn/problems/trapping-rain-water/description/?envType=study-plan-v2&envId=top-100-liked)

- 每个柱子 [左边第一个比他大的元素，右边第一个比他大的元素] -> 凹槽

更新 2026.2.6

他妈的这题困扰了我一个晚上，我最开始以为是纵向求解，即求每个方块上面的雨水面积。问题就是单调递增栈能得到右面第一个大于他的元素，得不到左面第一个大于他的元素，只能得到左面第一个大于等于的（没错，是包括等于的），因此纵向求解就没办法了

![image-20260206103903448](.\image-20260206103903448.png)

⬆️这种应该只能是求左面**最大的**和右面**最大的**元素，单调栈没办法，并且对于序号6来说，你操作一遍就发现序号6左面的元素是4，因为序号5弹出去之后序号4和序号6是挨着的......

⭐Carl提供了正确的思路——**横向**求解

![image-20260206104313326](.\image-20260206104313326.png)

这样解决了上述问题，左面的元素等于也没关系！！（序号6）

终于做出来了，代码如下⬇️

```python
class Solution(object):
    def trap(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        left_first_max = [0] * len(height)
        right_first_max = [0] * len(height)
        stack = []
        for index in range(0, len(height)):
            if not stack or height[index] <= height[stack[-1]]:
                stack.append(index)
            else:
                while stack and height[index] > height[stack[-1]]:
                    x = stack.pop()
                    right_first_max[x] = index
                    if not stack:
                        left_first_max[x] = -1
                    elif stack[-1]:
                        left_first_max[x] = stack[-1]
                stack.append(index)
        if stack:
            for _ in range(0, len(stack)):
                index = stack.pop()
                right_first_max[index] = -1
                if not stack:
                    left_first_max[index] = -1
                else:
                    left_first_max[index] = stack[-1]
        # 开始计算雨水面积，横向求解
        sum_rain = 0
        for i in range(0, len(height)):
            if left_first_max[i] == -1 or right_first_max[i] == -1: # 如果左边或者右面没有元素，那么不接雨水
                continue
            sum_rain += (min(height[left_first_max[i]], height[right_first_max[i]]) - height[i]) * (right_first_max[i] - left_first_max[i] - 1)
        return sum_rain
```



