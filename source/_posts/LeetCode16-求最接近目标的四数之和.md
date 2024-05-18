---

layout: LeetCode15-求最接近目标的四数之和

title: LeetCode15-求最接近目标的四数之和

date: 2023-03-02 23:49:38

tags: LeetCode

categories: Web


top: 16

path: /article/leetcode16

abbrlink: 1677767745

---

# LeetCode16-求最接近目标的四数之和



![image-20230314223435630](https://gitee.com/fadeway32/fadeway32/raw/master/img/202303142234703.png)

解答 ： 

参考三数之和 利用 双指针+剪枝 的做法

~~~java
class Solution{
    
    
    	//LeetCode15-求最接近目标的三数之和    
        public List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> ans = new ArrayList<>();
        if(nums == null || nums.length < 4){
            return ans;
        }
        Arrays.sort(nums);
        int length = nums.length;
        for(int i = 0;i<length-3;i++){
            if(i > 0 && nums[i] == nums[i-1]){
                continue;
            }
            // 剪枝
            if((long)nums[i]+nums[i+1]+nums[i+2]+nums[i+3] > target){
                break;
            }
            // 最大的数组结果 小于预期值
            if((long)nums[i]+nums[length-3]+nums[length-2]+nums[length-1] < target){
                continue;
            }
            // 另外一个循环
            for(int j=i+1;j<length-2;j++){
                if(j >i+1 && nums[j] == nums[j-1]){
                    continue;
                }
                // 考虑数值溢出的情况
                if((long)nums[i]+nums[j]+nums[j+1]+nums[j+2] > target){
                    break;
                }
                if((long)nums[i]+nums[j]+nums[length-1]+nums[length-2] < target){
                        continue;
                }
                int l = j+1; int r = length-1;
                while(l < r){
                    long sum = (long) nums[l] +nums[r]+nums[i]+nums[j];
                    if(sum == target){
                        ans.add(Arrays.asList(nums[i],nums[j],nums[l],nums[r]));
                        while(l < r && nums[l] ==nums[l+1]){
                            l++;
                        }
                        l++;
                        while(l < r && nums[r] == nums[r-1]){
                            r--;
                        }
                        r--;
                    }else if(sum < target){
                        l++;
                    }else{
                        r--;
                    }
                }



            }

           
        
    }
         return ans;
    }
}

~~~

