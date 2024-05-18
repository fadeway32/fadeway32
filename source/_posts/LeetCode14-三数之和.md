---

layout: LeetCode14-三数之和

title: LeetCode14-三数之和

date: 2023-03-02 23:49:36

tags: LeetCode

categories: Web


top: 14

path: /article/leetcode14

abbrlink: 1677767743

---

# LeetCode14-三数之和

![image-20230307225223682](https://gitee.com/fadeway32/fadeway32/raw/master/img/202303072252744.png)

思路：

1、定义收集的list

2、对数组进行排序

3、特殊情况判断 对于 数组最小值 >0 提前返回  或者数组的长度小于3

4、需要满足i 、j、k不同时相等

5、然后遍历。判断左右的情况 定义 左右指针 进行指针的移动

6、对于sum的结果 =0 >0 <0的三种情况 指针的移动

7、返回收集的list

~~~java
class Solution{
    
    
    public List<ArrayList<Integer>> collectSumIsZero(int[] array){
         List<ArrayList<Integer>> ans = new ArrayList<>();
		 if(array == null || array.length() == 0){
             return ans;
         } else{
             if(array.length < 3 || array[0] > 0){
                 return ans;
             }
         }
        Arrays.sort(array);
    
		for(int i=0;i<array.length;i++){
            if(i >1 && i < array.length-1;array[i] == array[i-1]){
                continue;
            }
            int l= i+1;
        	int r = array.length-1;
            while(l < r){
                int sum = array[i] + array[l] + array[r];
                if(sum == 0){
                    list.add(Arrays.asList(array[i]，array[l]，array[r]));
                    // 过滤  l++重复数据
                    while(l<r and array[l]==array[l+1]){
                        l=l+1; 
                     }
                    // 过滤  r--重复数据     
                    while(l<r and array[r]==array[r-1]){
                        r=r-1;
                    }
                        
                    r--;
                    l++;
                }else if(sum > 0){
                    r--;
                }else{
                    l++;
                }
            }
        }
        return ans;
    }
    
    
    
}
~~~

