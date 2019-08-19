
# leetcode

# 第11题，

一个数组里面的数字代表柱状图，求最大的存水面积即两个值中短的一个作为宽，两个值数组中的距离作为长，求最大的面积
两种解法，一种暴力双循环计算面积
另一种就是用双指针法，从数组的头尾移动指针求最大的面积。因为宽取最小值，所以要值小的移动，毕竟面积的长一开始是最大的，后面越来越小。
/**
 * @param {number[]} height
 * @return {number}
 */
var maxArea = function(height) {
    //推荐使用双指针法，在数组头部尾部分别取值然后按照取较高的值移动指针
    var left=0, right= height.length-1, max =0;
    while(left < right){
    var tmp=(right-left)*Math.min(height[right],height[left]);
    max=Math.max(tmp,max);
    if(height[right]>height[left]){
        left++;
    }else{
        right--
    }
    }
    return max;
};

# 第15题
如何取数组中的3个数，使和为0，并且不重复。
思想部分：（1）类似于2数之和用暴力法破解（2）利用哈希表，对于前端就是用map数据结构，先确定一个数，然后找其他两个数，如果已经在MAP中就找到了，不在的话就把这两个数登记（3）最后一种也是最优的想法，先将数组排序，然后依次取最小值，然后将剩下部分的数组用快排一样的思想前后逼近，最后求得是否0；然后还要加一些特殊情况的判定条件；例如最大值小于0或者最小值大于0.
 var threeSum = function (nums) {
      let res = []
      let length = nums.length;
      nums.sort((a, b) => a - b) // 先排个队，最左边是最弱（小）的，最右边是最强(大)的
      if (nums[0] <= 0 && nums[length - 1] >= 0) { // 优化1: 整个数组同符号，则无解
        for (let i = 0; i < length - 2;) {
          if (nums[i] > 0) break; // 优化2: 最左值为正数则一定无解
          let first = i + 1
          let last = length - 1
          do {
            if (first >= last || nums[i] * nums[last] > 0) break // 两人选相遇，或者三人同符号，则退出
            let result = nums[i] + nums[first] + nums[last]
            if (result === 0) { // 如果可以组队
              res.push([nums[i], nums[first], nums[last]])
            }
            if (result <= 0 ) { // 实力太弱，把菜鸟那边右移一位
              while (first < last && nums[first] === nums[++first]){} // 如果相等就跳过
            } else { // 实力太强，把大神那边右移一位
              while (first < last && nums[last] === nums[--last]) {}
            }
          } while (first < last)
          while (nums[i] === nums[++i]) {}
        }
      }
      return res
    }
