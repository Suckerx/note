## 认识复杂度和简单排序算法

![1666078028807](algorithm.assets/1666078028807.png)

**冒泡排序：**

比较0 和 1 位置上的数大小，然后交换，然后比较1 和 2 位置上的数交换，依次类推，第二遍从1 开始，1 和 2 比较后交换

![1666081093445](algorithm.assets/1666081093445.png)

因此是等差数列，时间复杂度为O(n^2)

![1666081184424](algorithm.assets/1666081184424.png)

代码：

![1666081288048](algorithm.assets/1666081288048.png)

异或运算：相同为0，不同为1，或者理解为不进位相加

![1666081407183](algorithm.assets/1666081407183.png)

不开辟额外空间交换两个数，**但是要保证a和b指向的内存不同**，因此在上面那个方法中，**i一定不能等于j**

![1666081570256](algorithm.assets/1666081570256.png)

**面试题：在一堆数中，有一个数出现了奇数次，其他数都出现了偶数次，找出这个奇数次的数**

![1666081981177](algorithm.assets/1666081981177.png)

思路：使用异或运算，每个数都跟eor异或，最终得到就是那个奇数次的数

![1666082020110](algorithm.assets/1666082020110.png)

**面试题：在一堆数中，有两个数出现了奇数次，其他数都出现了偶数次，找出这两个奇数次的数**

![1666083510316](algorithm.assets/1666083510316.png)

在一堆数中进行异或，最终结果就是a^b，他们肯定不等于0，表示a和b用二进制表示至少有一位是1，即有一个位置a和b不相同，假设为第8位，根据这个第8位将原数组进行分类，分为第8位是1的数和第8位是0的数，而a和b只可能分别在两边，此时用一个变量去异或第8位是1的数，此时这个变量一定是a或者b，再让他和eor进行异或，即可得到另一个数

提取一个数最右侧的1：

![1666084222500](algorithm.assets/1666084222500.png)

![1666084231117](algorithm.assets/1666084231117.png)



![1666084329319](algorithm.assets/1666084329319.png)

**插入排序**

![1666084393362](algorithm.assets/1666084393362.png)

![1666085142768](algorithm.assets/1666085142768.png)

一直往前面比较，直到比前面大就结束

**二分法**

![1666085341263](algorithm.assets/1666085341263.png)

局部最小值就是 i 位置的数要小于其左右两边的数，求局部最小值也可以用二分

**对数器**

![1666096804589](algorithm.assets/1666096804589.png)

随机数组方法

![1666097147483](algorithm.assets/1666097147483.png)

![1666097181979](algorithm.assets/1666097181979.png)

## 认识O(NlogN)的排序

**递归**

![1666098253661](algorithm.assets/1666098253661.png)

 求中点位置防止溢出：右移一位

![1666098374004](algorithm.assets/1666098374004.png)

![1666098429150](algorithm.assets/1666098429150.png)

master 公式的介绍：只要是子问题等规模就可以用master公式求解

母问题N个数据，子问题每次都是 N/b 的规模，a指的是子问题调用次数，后面的是除了子问题外剩下过程的时间复杂度

![1666099083933](algorithm.assets/1666099083933.png)

所以求出来是这样

![1666100229210](algorithm.assets/1666100229210.png)

求解时间复杂度：

![1666160016678](algorithm.assets/1666160016678.png)

**归并排序**

![1666160159428](algorithm.assets/1666160159428.png)

![1666160387992](algorithm.assets/1666160387992.png)

![1666160452617](algorithm.assets/1666160452617.png)

思路：将数组分为两边，左右都排序完毕后merge合并，双指针比较，谁小谁进入help数组，直到一方越界，然后将剩下的全部复制进help数组

**拓展**

![1666161607608](algorithm.assets/1666161607608.png)

求小和可以逆向思考，每次比较找右边比他大的数，比如1和3合并的时候，在1的右边有一个数比1大，所以记录有1个1，134合并时，在1的右侧有找到一个4比1大，再记录一个1，3和4比较时，3的右边有个数比3大，所以记录1个3，以此类推求出来也是小和

![1666163210485](algorithm.assets/1666163210485.png)

求小和的合并过程中，如果是两边相等，一定要保证是右组先合并进去，否则无法计算小和

![1666163903763](algorithm.assets/1666163903763.png)

process函数中return的是左侧排序求小和的数量+右侧排序求小和的数量+merge合并时产生小和的数量

拷贝的时候只有严格左组比右组小才拷贝左组，否则拷贝右组

![1666164429590](algorithm.assets/1666164429590.png)

逆序对也是一样的思路

**快速排序**

![1666165024588](algorithm.assets/1666165024588.png)

![1666182181181](algorithm.assets/1666182181181.png)

问题一思路：开始的时候设定一个变量表示小于等于的区域的边界，然后边界刚开始在最左边，然后从数组第一个数开始比较，若小于等于num，则当前这个数和边界区的下一个数交换，然后小于等于边界区右扩，i++到下一个数，如果是大于，则直接指针下一个

![1666182514347](algorithm.assets/1666182514347.png)

问题二思路：两个边界，三种判断情况，第三种是 i 原地不动，当大于区域和 i 相等时停止

**快排1.0版本**

![1666182885872](algorithm.assets/1666182885872.png)

在数组中最后一个数，放到小于等于区域的最后一个位置，然后小于等于区域去递归，大于区域也递归，每次排好一个数，就能有序

**快排2.0版本**

利用荷兰国旗问题



思路：一开始在整个范围上用最后一个数做划分，让前面的范围做到都是小于5，中间都是等于5，右边是大于5，让5和大于5的第一个数交换，然后在左右递归

![1666183304726](algorithm.assets/1666183304726.png)

这两种，时间复杂度都是O(N^2)

![1666335531263](algorithm.assets/1666335531263.png)

**快排3.0**

随机选一个数，和最后一个数交换，作为划分

此时时间复杂度为O(NlogN)

![1666184335652](algorithm.assets/1666184335652.png)

partition返回的数组长度一定为2

![1666184447403](algorithm.assets/1666184447403.png)

返回的是12和13，表示返回的是等于区域的左边界和右边界

p[0]是等于区域的左边界，所以-1去左边递归

partition就是荷兰国旗问题

![1666184515520](algorithm.assets/1666184515520.png)

## 详解桶排序以及排序内容总结

**堆**

![1666335848491](algorithm.assets/1666335848491.png)

完全二叉树：节点从左到右的填充的就是完全二叉树，只有左节点也叫完全二叉树，但是略过左节点直接到右节点就不是完全二叉树

数组转完全二叉树的关系：

除法是向下取整

![1666336818574](algorithm.assets/1666336818574.png)

转化大根堆，就是每个数跟自己父亲比较，若大则交换

![1666337173736](algorithm.assets/1666337173736.png)

如果需要删掉大根堆的头节点，那么我们将堆最后一个数字移到头节点，然后堆的大小-1，然后循环用头节点比较他的两个字节点中的最大值，若小于则交换，重复此操作，保证一直是堆结构 

![1666337568531](algorithm.assets/1666337568531.png)

**堆排序**

![1666338178975](algorithm.assets/1666338178975.png)

思路：先用heapInsert将数组调整为堆结构，然后重复将最后一位跟头节点交换后，将0位置做heapify操作，最后即可排序完毕，成为从小到大排序

算法整体复杂度为：O(N*logN)

细节再优化：

将数组调整为堆结构的代码可以再优化成这样，从最后开始往下做heapify调整(即每个子树先调整为大根堆)

![1666338986207](algorithm.assets/1666338986207.png)

这一步的复杂度是O(N)

![1666338921044](algorithm.assets/1666338921044.png)

 拓展题目

![1666339118419](algorithm.assets/1666339118419.png)

有些题目，只需要一个小根堆结构，不需要修改其中的值之类的操作，就可以用系统提供的堆结构函数，如果需要更复杂的调整，则手写的效率更高

![1666345354135](algorithm.assets/1666345354135.png)

思路：先把前几个数放到小根堆中，每次弹出一个数放到数组中，然后新加一个数放到堆中，每次弹出的就是最小值

**比较器**

![1666363847555](algorithm.assets/1666363847555.png)

![1666592753793](algorithm.assets/1666592753793.png)

可以改写成容易理解的样子

![1666592820385](algorithm.assets/1666592820385.png)

就是如果第一个参数更小就返回负数，第一个更大则返回正数，这就是升序

![1666593065643](algorithm.assets/1666593065643.png)

如果是Id降序则用第二个参数-第一个参数

![1666593122750](algorithm.assets/1666593122750.png)

比较器还能用在堆之类的结构中，传个比较器

大根堆就是用第二个参数减第一个

![1666593872284](algorithm.assets/1666593872284.png)

复杂数据，自己定义的类，用这种方式会很方便

**桶排序**

桶可以是任意数据结构，这题我们用队列

对这几个数进行补全，补成3位数，然后按照个位数放到桶里

![1666594735940](algorithm.assets/1666594735940.png)

然后从头开始倒出来

![1666594752384](algorithm.assets/1666594752384.png)

先进桶的先出来，队列先进先出

然后根据十位数再放进桶里面

![1666594804548](algorithm.assets/1666594804548.png)

再倒出来

![1666594819163](algorithm.assets/1666594819163.png)

再按照百位数进桶

![1666594832513](algorithm.assets/1666594832513.png)

再倒出来就排好序了

![1666594846138](algorithm.assets/1666594846138.png)

![1666595099362](algorithm.assets/1666595099362.png)

![1666595115177](algorithm.assets/1666595115177.png)

digit参数表示这些数中最大的数字有几个十进制位

![1666595166072](algorithm.assets/1666595166072.png)

![1666596160217](algorithm.assets/1666596160217.png)

这里不是用桶搞得，是优化了很多，但是思想是这样得，用得是词频表，个位数是几就在下表处++

![1666595329327](algorithm.assets/1666595329327.png)

然后让他变成前缀和数组，所以现在下标2的4变成了个位数小于等于2的数有4个

![1666595437309](algorithm.assets/1666595437309.png)

此时我们从右往左看，062这个数，是最右侧，他一定是最后一个进桶的，根据先进先出，而个位数小于等于2的数只有4个，所以062一定是在help数组的下标3位置(即第四个数)，然后词频-1

![1666595655355](algorithm.assets/1666595655355.png)

以此类推

![1666595708453](algorithm.assets/1666595708453.png)

**排序算法的稳定性及其汇总**

![1666596346803](algorithm.assets/1666596346803.png)

稳定性指的是，相同的元素能否保证在排序完后保证其原来次序不变

![1666597159455](algorithm.assets/1666597159455.png)

一般都会选择快速排序，能用快排就用快排

![1666597318865](algorithm.assets/1666597318865.png)

![1666597524621](algorithm.assets/1666597524621.png)

例如快排加上一段

![1666597559468](algorithm.assets/1666597559468.png)

就是小样本量时，我们直接用插入排序，更快，这种叫综合排序

系统提供的Array.sort，如果是基础数据类型，就会用快排，如果是非基础数据类型就用归并，因为要稳定性

## 链表

![1666598588661](algorithm.assets/1666598588661.png)

hashSet没有值，只有key，hashMap有value，第一次是添加，第二次是更新

哈希表的所有增删改查时间复杂度都是常数级别

![1666598725271](algorithm.assets/1666598725271.png)

不是基础类型，内存占用就是8字节

![1666598931104](algorithm.assets/1666598931104.png)

所以这里的nodeA和nodeB不一样

![1666599917233](algorithm.assets/1666599917233.png)

有序表，根据key组织

有序表的增删改查都是O(logN)

![1666600055763](algorithm.assets/1666600055763.png)

不是基础类型，没给比较器会报错

![1666600135968](algorithm.assets/1666600135968.png)

**单链表**

![1666600204581](algorithm.assets/1666600204581.png)

![1666600272499](algorithm.assets/1666600272499.png)

如果有换头操作，则需要返回头节点

![1666600727143](algorithm.assets/1666600727143.png)

```java
package com.zzw.test;

/**
 * @program: HashMapTest
 * @description: 双向链表反转
 * @author: zhaozhenwei
 * @create: 2021-05-30 10:55
 **/
public class DoubleListInversion {

    public static void main(String[] args) {
        DoubleNode listInversion = createListInversion();
        printListInversion(listInversion);
        printListInversion(inversion(listInversion));

    }

    /**
     * 链表反转
     *  currentNode 当前处理的节点
     *  previous    处理的上一个节点     初始情况下为null
     *  next        要处理的下一个节点    初始情况下为第一个节点的下一个节点
     *   通过死循环进行处理，跳出判断放在循环内
     *   将当前节点的上一个节点currentNode.previous执行要处理的下一个节点next
     *   将当前节点的下一个节点currentNode.next指向上次处理的节点previous
     *   此时当前节点处理完成，进行下一个节点处理的初始化
     *      previous指向当前处理的节点currentNode
     *      判断当前节点currentNode的下一个节点next是否为null，如果为null说明当前节点currentNode是最后一个节点，跳出循环
     *          如果不为null，将下一个节点指向next.next
     * @param node
     * @return
     */
    public static DoubleNode inversion(DoubleNode node) {
        if (null == node) {
            throw new RuntimeException("反转链表起始节点不能为null");
        }
        // 当前节点
        DoubleNode currentNode = node;
        // 上个节点
        DoubleNode previous = null;
        // 下个节点
        DoubleNode next = currentNode.next;
        while (true) {
            currentNode.previous = next;
            currentNode.next = previous;
            previous = currentNode;
            if (null == next) {
                break;
            }
            currentNode = next;
            next = next.next;
        }
        return previous;
    }

    /**
     * 打印链表
     * @param node
     */
    static void printListInversion(DoubleNode node) {
        DoubleNode currentNode = node;
        while (null != currentNode) {
            System.out.println(currentNode);
            currentNode = currentNode.next;
        }
        System.out.println();
    }

    /**
     * 创建链表
     * @return
     */
    static DoubleNode createListInversion() {
        DoubleNode n1 = new DoubleNode(1);
        DoubleNode n2 = new DoubleNode(2);
        DoubleNode n3 = new DoubleNode(3);
        DoubleNode n4 = new DoubleNode(4);
        DoubleNode n5 = new DoubleNode(5);

        n1.previous = null;
        n1.next = n2;

        n2.previous = n1;
        n2.next = n3;

        n3.previous = n2;
        n3.next = n4;

        n4.previous = n3;
        n4.next = n5;

        n5.previous = n4;
        n5.next = null;

        return n1;
    }


}



class DoubleNode {
    int value;
    DoubleNode previous;
    DoubleNode next;
    public DoubleNode(int value) {
        this.value = value;
    }

    @Override
    public String toString() {
        return "DoubleNode{"
                + "previous: " + (null == previous ? "null" : previous.value) +
                "\tvalue=" + value
                + "\tnext:" + (null == next ? "null" : next.value) + "}";
    }
}

```



![1666600353231](algorithm.assets/1666600353231.png)

谁小谁移动，相同就打印然后一起移动

![1666601112618](algorithm.assets/1666601112618.png)

![1666601171484](algorithm.assets/1666601171484.png)

用个栈然后遍历比较就行

可以只放右侧进栈就行，可以省一半空间，此时需要使用快慢指针技巧，快指针一次走两步，慢指针一次一步，快指针到终点的时候，慢指针就在中间了

![1666601536490](algorithm.assets/1666601536490.png)

可能边界条件不同，还分奇偶

如果只用几个变量，不用额外空间

![1666601713809](algorithm.assets/1666601713809.png)

使用快慢指针，慢指针到中点，然后继续遍历时，让中点指向空，其他的反转，然后用变量记住头节点和尾节点，然后他们同时往中间走，每一步都一样即可，有一个走到空就停，但是返回结果前要把链表恢复

方法一：

![1666601905145](algorithm.assets/1666601905145.png)

![1666601952442](algorithm.assets/1666601952442.png)

方法二：

![1666601993204](algorithm.assets/1666601993204.png)![1666602120750](algorithm.assets/1666602120750.png)



![1666602161560](algorithm.assets/1666602161560.png)

思路：笔试就直接申请一个Node类型数组，然后在数组中进行划分，然后再遍历链接即可

进阶：使用6个变量，分别是小于部分的头指针和尾指针，等于部分的头指针和尾指针，大于部分的头指针和尾指针，一开始都指向空，在遇到第一个时则将头尾都指向它，然后第二个时，将第一个指向第二个，然后尾指针指向第二个，最终让小于部分的最后那个节点指向等于部分的头节点，等于部分的尾节点指向大于部分的头节点即可

![1666602499890](algorithm.assets/1666602499890.png)

注意一定要考虑边界，有可能没有小于部分

方法一：

![1666602746364](algorithm.assets/1666602746364.png)

![1666602789312](algorithm.assets/1666602789312.png)

![1666602802698](algorithm.assets/1666602802698.png)

方法二：

![1666602723500](algorithm.assets/1666602723500.png)

![1666602868725](algorithm.assets/1666602868725.png)

![1666602881912](algorithm.assets/1666602881912.png)



![1666602916913](algorithm.assets/1666602916913.png)

使用一个map，key为老节点，value为新复制的节点，遍历每一个老节点将其放到map中，然后开始设置指针连接方向

![1666614270415](algorithm.assets/1666614270415.png)

方法二：不用map，直接用新的节点接到老节点后面，不管rand指针

![1666614460384](algorithm.assets/1666614460384.png)

然后，遍历的时候一对一对拿，拿1和1`，只考虑其rand指针，通过1的rand指针得到3，此时3后面就是1撇得rand指针3撇，最后分离next指针

![1666614717925](algorithm.assets/1666614717925.png)

![1666614760435](algorithm.assets/1666614760435.png)

