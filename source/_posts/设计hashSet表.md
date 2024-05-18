
---

layout: 设计hashSet表

title: 设计hashSet表

tags: Web

categories: Web

top: 34

path: /article/1713100397

abbrlink: 1713100397



date: 2024-04-14 21:14:00


--- 

# 设计hashSet表



不使用任何内建的哈希表库设计一个哈希集合（HashSet）。



实现 `MyHashSet` 类：

- `void add(key)` 向哈希集合中插入值 `key` 。
- `bool contains(key)` 返回哈希集合中是否存在这个值 `key` 。
- `void remove(key)` 将给定值 `key` 从哈希集合中删除。如果哈希集合中没有这个值，什么也不做。

**示例：**

```java
输入：
["MyHashSet", "add", "add", "contains", "contains", "add", "contains", "remove", "contains"]
[[], [1], [2], [1], [3], [2], [2], [2], [2]]
输出：
[null, null, null, true, false, null, true, null, false]

解释：
MyHashSet myHashSet = new MyHashSet();
myHashSet.add(1);      // set = [1]
myHashSet.add(2);      // set = [1, 2]
myHashSet.contains(1); // 返回 True
myHashSet.contains(3); // 返回 False ，（未找到）
myHashSet.add(2);      // set = [1, 2]
myHashSet.contains(2); // 返回 True
myHashSet.remove(2);   // set = [1]
myHashSet.contains(2); // 返回 False ，（已移除）
```



借鉴 宫水三叶大佬

~~~java
class MyHashSet{
    
    public  Node[] nodes=  new Node[10009];
    
    
    public void add(int key){
      int index=   getIndex(key);
      Node curNode = nodes[index];
      Node temp = curNode;
      if(curNode != null){
      	   Node prev = null;
           while(temp != null){
              if(temp.key == key){
                  return;
              }
              prev = temp;
              temp  =temp.next;
          }
          temp  = prev;
      }
      Node node = new Node(key);
        
        // 头插
//        node.next=curNode;
  //      nodes[index] = nodes;
    	// 尾插
        if(temp != null){
            temp.next =node;
        }else{
            nodes[index] = node;
        }

        
    }
    
    
    
    
    public boolean contains(int key){
          int index=   getIndex(key);
	     Node curNode = nodes[index];
 		 if(curNode != null){
			Node next= null;
          	while(curNode != null){
   				if(curNode.key == key){
                    return true;
                }
                curNode = curNode.next;   
            }    
         }
        return false;
           
           
    }
    
    public void remove(int key){
          int index=   getIndex(key);
	     Node curNode = nodes[index];
          if(curNode != null){
              Node prev = null;
              while(curNode != null){
                  if(curNode.key == key){
                      // 判断前驱节点存在
                      if(prev != null){
                          prev.next = curNode.next;
                      }else{
                          nodes[index] = curNode.next;
                      }
                  }
                  prev = curNode;
                  curNode =curNode.next;
              }
              
              
          }
       
             
    }
    
    
    static class Node{
        private int key;
        private Node next;
        private Node(int key){
            this.key = key;
        }
    }
    
    // 实现getindex寻找key的hash捅位置
    int getIndex(int key){
        // 因为 nodes 的长度只有 10009，对应的十进制的 10011100011001（总长度为 32 位，其余高位都是 0）
        // 为了让 key 对应的 hash 高位也参与运算，这里对 hashCode 进行右移异或
        // 使得 hashCode 的高位随机性和低位随机性都能体现在低 16 位中
        int hash  = Integer.hashCode(key);
        hash  ^=  hash >>> 16;
        return hash % nodes.length;
    }
    
}


~~~

