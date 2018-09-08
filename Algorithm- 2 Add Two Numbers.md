# Algorithm- 2 Add Two Numbers
## 链接
[https://leetcode.com/problems/add-two-numbers/description/](https://leetcode.com/problems/add-two-numbers/description/)
## 内容
给两个链表，将他们依次相加输出结果，如下所示
```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
```
## 思路
相加满10的时候就向前进一位，只要碰到两个链表有一个没有next，就停下来，让最长的那个循环加下去

## 代码
```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution2 {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2){
        ListNode headNode = new ListNode(0);
        ListNode currentNode = headNode;
        while (l1.next != null && l2.next != null){
            int value = l1.val + l2.val + currentNode.val;
            if (value >= 10){
                currentNode.val = value % 10;
                currentNode.next = new ListNode(1);
            } else {
                currentNode.val = value;
            }
            l1 = l1.next;
            l2 = l2.next;
            if (currentNode.next == null){
                currentNode.next = new ListNode(0);
            }
            currentNode = currentNode.next;
        }

        int value = currentNode.val + l1.val + l2.val;

        if (value >= 10){
            currentNode.val = value % 10;
            currentNode.next = new ListNode(1);
        } else {
            currentNode.val = value;
        }

        while (l1.next != null){

            if (currentNode.next !=null){
                currentNode.next.val = currentNode.next.val + l1.next.val;
            } else {
                currentNode.next = new ListNode(l1.next.val);
            }
            if (currentNode.next.val >=10){
                currentNode.next.val = currentNode.next.val %10;
                currentNode.next.next = new ListNode(1);
            }
            l1.next = l1.next.next;
            currentNode = currentNode.next;
        }

        while (l2.next != null){
            if (currentNode.next !=null){
                currentNode.next.val = currentNode.next.val + l2.next.val;
            } else {
                currentNode.next = new ListNode(l2.next.val);
            }
            if (currentNode.next.val >=10){
                currentNode.next.val = currentNode.next.val %10;
                currentNode.next.next = new ListNode(1);
            }
            l2.next = l2.next.next;
            currentNode = currentNode.next;
        }

        return headNode;
    }
}
```

# Review - Uber Open Sources JVM Profiler for Tracing Distributed JVMs
## 链接
[https://www.infoq.com/news/2018/08/uber-jvm-profiler?utm\_source=infoq&utm\_medium=popular\_widget&utm\_campaign=popular\_content\_list&utm\_content=homepage](https://www.infoq.com/news/2018/08/uber-jvm-profiler?utm_source=infoq&utm_medium=popular_widget&utm_campaign=popular_content_list&utm_content=homepage)
## 内容
Uber开源了一个分布式的JVM分析工具用于分析他们Spark集群中的JVM环境，Uber的Spark集群使用了上千台机器，每台机器有几千个应用在同时执行，现在的JVM工具只能是针对系统级别的，Uber更想知道JVM中每一个应用的情况，更近一步可以知道每个方法的耗时或者在HDFS中的热点文件，然后有针对的进行优化。设计的也比较有扩展性，可以添加其他的分析器进行分析。

![图像 2018-9-8，下午9.19](media/15364129904388/%E5%9B%BE%E5%83%8F%202018-9-8%EF%BC%8C%E4%B8%8B%E5%8D%889.19.jpg)




## 点评 
这种需求要求我们对JVM有一个比较清楚的认识，并能够针对性进行分析开发，并且设计的时候不要只考虑当前的需求，还要设计得有扩展性。我觉得我们也需要这样一个工具，每次线上机器Full GC的时候只能人肉的去看日志，然后分析，并没有做到一个自动化的运维流程，而且做到方法级别的话会帮助我们更好的写出高质量的代码。

# Tip - 技术技巧
## 流水任务-抽象地确保最终一致性设计

![图像 2018-9-8，下午9.19 -1-](media/15364129904388/%E5%9B%BE%E5%83%8F%202018-9-8%EF%BC%8C%E4%B8%8B%E5%8D%889.19%20-1-.jpg)



## 适用场景
比如发表评论、发表文章这种对强一致性要求不高的场景

# Share 
我们应该成为一个“T”字型人才，在知识的深度和广度中首先选择深度
1. 做好现在手中该做的事。
2. 最好选择一个跟自己工作比较相关，且自己比较感兴趣的方向不断学习、研究下去，这就是“T”中的那一条竖线，这个阶段大概需要3年。
3. 后面需要扩充自己的知识面和软技能，比如演讲、沟通、写作等等，不断丰富自己，打开眼界
在职业生涯中，终身学习是必须的，另外就是英语，一定要好好练！！！


