---

layout: LeetCode15-求最接近目标的三数之和

title: LeetCode15-求最接近目标的三数之和

date: 2023-03-02 23:49:37

tags: LeetCode

categories: Web


top: 15

path: /article/leetcode15

abbrlink: 1677767744

---

# LeetCode15-求最接近目标的三数之和

<img src="https://gitee.com/fadeway32/fadeway32/raw/master/img/202303122155080.png" alt="image-20230312215508028" style="zoom:130%;" />

求解：

三层for循环 接近的sub的值、

~~~java
class Solution{
    
    public int threeSumClosest(int[] nums, int target) {
		// 保存和目标的差值
        int sub = Integer.MAX_VALUE;
        // 定义保存之和
        int sum =0;
        
        int length = nums.length;
        for(int i=0;i<length;i++){
            for(int j=i+1;j<length;j++){
                for(int k=j+1;k<length;k++){
                    if(Math.abs(nums[i]+nums[j]+nums[k]-target) < sub){
                        // 更新target 值
                        sum = nums[i]+nums[j] + nums[k];
                        sub = Math.abs(nums[i]+nums[j] + nums[k] -target);
                    }  
                    }
                }
            }
            
            return sum;
        }
        
    }
	// 双指针的思想
  	public int threeSumClosest2(int[] nums, int target) {
		Arrays.sort(nums);
        int nearNum = nums[0] + nums[1] + nums[2];
        // 保证最右边的数组不越界
       	for(int i=0;i< nums.length-2;i++){
            int l = 0; int r = nums.length-1;
            while(l<r){
                int targetNum = nums[l]+nums[i]+nums[r];
                if(Math.abs(targetNum - target ) <  Math.abs(nearNum -target )){
                    nearNum  = targetNum;
                }
                // 大于 
                if(targetNum >  target){
                    r--;
                }else if (targetNum < target){
                    l++;
                }else{
                    // 相等则是最接近的值
                    return target;
                }
            }
        }
        return nearNum;
        
        
    }
    
    
    
}
~~~

