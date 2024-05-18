
---

layout: leetcode01-two sum

title: LeetCode01-两数之和

date: 2023-02-15 22:08:30

tags: LeetCode

categories: Web

description: LeetCode 两数之和

top: 2

path: /article/leetcode01

abbrlink: 1305786654

---

# LeetCode01

![Two Sum](https://gitee.com/fadeway32/fadeway32/raw/master/img/20230215221612.png)

给定一个数组和一个目标和，从数组中找两个数字相加等于目标和，输出这两个数字的下标。


****

answer1:

~~~ javascript
    public int[] twoSum(int[] nums, int target) {
      Map<Integer,Integer> map=new HashMap<>();
      for(int i=0;i<nums.length;i++){
        int sub=target-nums[i];
        if(map.containsKey(sub)){
            return new int[]{i,map.get(sub)};
        }
        map.put(nums[i], i);
    }
    throw new IllegalArgumentException("No two sum solution");
  }

~~~