改天学学markdown。。。

目前进度(122/208)


LeetCode做题笔记

1.	Add two numbers：给定一个数集合和一个数，已知集合中有两个数的和是给定数，求这两个加数的index
方法1：暴力，n^2时间复杂度，不推荐
方法2：快速排序nlogn。按集合里数的两倍与target的大小关系对分。对每一个第一部分的数，在另外一个部分二分搜索第二个数：500~ms
方法3：hash，n的时间复杂度，最高纪录420ms

经验1：对hashMap的get和put都是非常耗时间的，尽量少做
经验2：方法2最好使用随机化快排，效率很高

2.	把两个链表表示的数加起来：最佳624ms，3%
用长一点的链表做基础，最多只需要new一个新节点
优化建议：进位尽量用数字。如果一个链到头了，另一个没到，应该沿着长链前进。如果进位是0就可以即刻返回，不需要继续前进。


3.	把一个整数数位逆转，注意符号，不能溢出
最好记录404ms，前5%
较好的算法已经附在code里
经验3：类库比较快。而且好像早上比较快？
官方提示：
To check for overflow/underflow, we could check if ret > 214748364 or ret < –214748364 before multiplying by 10. On the other hand, we do not need to check if ret == 214748364, why? 溢出是2147483647， 214748364乘10不溢出 

4.	手写atoi，一大堆判断。。。最好记录408ms，约为5%
	  经验4：如何经济的判断溢出
      经验5：让不合法的输入第一时间return 0;
	  经验6：对于javascript里那一堆isxxx的函数，对应在Java的Character类下
 
5.	求两个升序数组的中位数(8, hard)
网上绝大部分解法都是错误的，和我犯了一样的错误。三个小时啊啊啊啊啊白费了

经验7：求平均数应该除以2.0

错误算法：
分别求出序列A 和B 的中位数，设为a 和b，求序列A 和B 的中位数过程
1）若a=b，则a或b即为所求中位数，算法结束。
2）若a<b，则舍弃序列A中较小的一半，同时舍弃序列B中较大的一半,要求舍弃的长度相等；
3）若a>b，则舍弃序列A中较大的一半，同时舍弃序列B中较小的一半，要求舍弃的长度相等；
在保留的两个升序序列中，重复过程1）、2）、3），直到两个序列中只含一个元素时为止，较小者即为所求的中位数。
原因：应该在任何一个数列剩两个元素的时候就停止程序，因为有可能中位数恰好就是这两个元素的平均数，不能舍去。但这时要分析的情况太多，不优。

正确算法:主要思想就在于找到一个数，这个数前面有(n+m)/2个数

6.	给定一个有序序列，求不同的元素个数并且返回不同序列，要求原地返回，O(1)空间(26, easy)
15分钟，第一次就AC了略开心，最好记录406ms貌似是前1%！虽然这个时间不靠谱
没啥可优化的了，感觉几乎没有废代码

7.	括号匹配。(20, easy)
最好记录430ms，前10%。稍微用了点小聪明，不过不好（使用异常做判断）
经验8：使用Stack比使用数组效率高很多，对这个题而言
 
8.	判断一个数是不是回文数，不能用额外空间（这点好奇怪，不用额外空间连循环都没法跑了）（9, easy）
经验？：真的会有公司考这么简单？

9.	归并K个有序链表。使用堆来做，一开始把K个链表的第一个元素放进数组，然后建堆。之后取出第一个元素（如果这个元素是nil元素，直接退出）放进归并后的链表，再从这个元素所在的链表取第一个元素放到原来元素的位子上，然后重新维护堆性质。如果那个链表已经没有元素，那就插入一个nil元素。

趁机用了用泛型方法，真好使！哨兵nil也不错，感谢算法导论！

经验10：维护堆性质后不能减少length，因为不能保证length-1位的元素一定是nil

10.	找出一组数里那个单蹦的（其他都是一对）
方法一：使用BitSet，正负分开统计
方法二(非常完美)：遍历数组，对每一个元素做异或
经验11：BitSet好东西，真心好！谁用谁知道！

11.	找到一个字符串里最长的无重复字符的子串（leetcode第3题，medium）
O(N)的算法，时间最好280ms，大概前2%左右，这个算法已经不能更优化了。

大概的思路是：找到一对相同的之后，计算这一对的后面那个与j（上一对的前面那个+1）之间的距离。为了不单独处理所以给了j-1的初始值。（其实这个算法一开始有两个指针，后来我发现好像一个指针也能跑，但是两个到一个指针稍稍有点难说这个区别）
 
12.	把输入的字符串排成Z字形输出（leetcode第6题，easy），没啥可优化的。
O(N)的算法，时间最好429ms，大概前5%左右。


13.	求一个无符号数的二进制表示有多少个1.（leetcode第191题，easy）。最好时间
主要难点是位运算吧。而且Java直接给负数略坑啊
	 
经验12：取余n等于& (n-1)，当n是2的幂的时候。
经验13：long做直接数运算时，直接数后面要加L表示这个数用LONG。

14.	将数组向右旋转。（LeetCode第189题）
方法：先reverse前k个元素，再reverse后n-k个元素，最后reverse所有的元素。这个算法只使用O(1)的空间，原载于编程珠玑。我只能说，精彩而美妙！
 
15.	把一个整数的二进制表示倒过来并输出这个新二进制对应的整数。（LeetCode190， easy）。最好成绩300ms，前30%。还是2的幂使用位操作可以大大简化

16.	归并两个链表，leetcode 23，easy。太简单了没啥可说。。。。
 
17.	在一个数组里寻找所有满足a+b+c=0的a,b,c。LeetCode 15，Medium
a)	方法一：先用0做pivot，对所有的数进行一次partition，区分开正负数。然后对于每一个数，在符号相反的区域内调用two sum。这个算法可行，时间复杂度理论上是O(N^2)，但是用Set之类的数据结构比较多，拖慢了整体的速度。最后无论怎么优化都没成功。
b)	方法二：先对数组做快排，然后从最小的数开始用I，j做循环，在J后面用二分查找找第三个数
c)	方法三：对方法二的优化，二分查找应该返回比要查找的数小的最大的数，这样之后的二分查找能够更快完成，我以后抽空优化~

18.	创建一个Stack，要求push pop top和 getMin都要在常数时间内完成。（LeetCode155， easy）
主要想法：两个栈一个存最小值一个是普通栈，最小栈要求只压入不大于栈顶元素的元素。出栈时若两站栈顶元素相同则同时pop，否则只pop普通栈的元素

19.	在一列数里寻找三个数a, b和c，要求a+b+c最接近target（Leetcode16, Medium）
把3sum的binarySearch改成二分查找最接近的元素就好了，整体算法不变。不跳过重复元素。

20.	删去一个list里倒数第n个，one-pass (LeetCode19, Easy)
三个指针一前一后一头，搞定

21.	一个排好序的数组被右移了，搜索一个数字(LeetCode33, Easy)
a)	线性搜索，不说了，投机取巧. O(N)
b)	线性搜索到分界线，在分界线后面二分搜索。也是O(N)
c)	改进后的二分搜索：分类讨论思想，有七种情况
i.	如果mid和target一样，那不用找了，return
ii.	如果mid比target小，分三种情况讨论
1.	Mid比right小，target也比right小，说明target在以mid+1为起始，right为终止的已排序序列里，直接调用标准二分查找即可。
2.	Mid比right小，target比right大，说明mid右侧的上升序列里没有target，应该在左侧继续查找：right=mid-1;
3.	Mid比right大，说明mid左边的上升序列里没有target，应该在右侧继续查找：left=mid+1；
2和3都不能使用标准二分查找，因为序列不是排好序的.
iii.	如果mid比target大，分三种情况讨论，和上面三种情况差不多
这个方法所有的情况都能保证O(LgN)的时间复杂度，应该是最优了。

22.	找到一个字符串数组里所有字符串的最长公共前缀。(LeetCode14, Easy)
实在太简单。。。我从+=和StringBuilder试了试，感觉时间差不多。不过还是应该用StringBuilder
23.	交换链表相邻两个node.(LeetCode24, medium)
a)	四个指针一点一点往前挪。
b)	递归算法。网上看到的
 
24.	右移链表（leetCode 61， medium）
a)	跟删除差不多，先过一遍确定长度，再一前一后的往前挪
b)	另一个很不错的算法，在论坛里看到的：先首尾相连，再在移动之后斩开

25.	4sum, 找到a,b,c,d四个数要求他们的和是target
a)方法一：先对数组做快排，然后从最小的数开始用I，j，k做循环，在k后面用二分查找找第四个数。当出现没可能的情况的时候剪枝，时间复杂度O(N^3*lgN)
b)方法二：先对数组做快排，然后从最小的数开始用I，j做循环，在j后面用front，end两个指针夹逼。时间复杂度O(N^3)
虽然b的时间复杂度优一点，但是跑出来时间差的不多。

26.	判断两个二叉树是否相等(Leetcode 100, easy)。太基本了不说了。

27.	判断两个二叉树是否对称(Leetcode 101, easy)。
a)	递归方法很简单，调用100的方法传入对称的子树即可
b)	非递归方法
i.用一个栈，在每一个循环中先取出栈顶的两个元素做比较，再把这两个元素的子树按左左右右、左右右左的顺序push进去
ii.	用两个栈，非递归前序遍历左树和右树（右树先遍历右子树），最后全弹出来比较即可

28. 对一个链表做插入排序。基本就是把一个链表的node一个一个插入另一个链表里(LeetCode147, medium)

29.	求二叉树最大深度(Leetcode 104, easy)。太基本了不说了。

30. 求二叉树最小深度(LeetCode 111, easy) 尝试用非递归的方法做。其实就是用一个队列做广度优先搜索，找到第一个叶子节点就返回。

31. 二分查找一个数，找不到就返回他应该在的位置(LeetCode35, medium)
这个题还medium是几个意思。。。除了把正规二分查找的-1改成left我没看见其他的需要改代码的地方。。。。

32. 找到一个数组里的多数元素。（LeetCode 169, easy）
说真的，这个才应该是Hard，因为有两个特别好的算法.O(N)时间复杂度
a) 摩尔投票算法，用一个counter解决问题，我在算法书上看到过
b) 位运算重建多数元素

32. 检查一个链表有没有环。(LeetCode141, medium)
我的方法是把节点拆散然后指向一个哨兵。O(N)的时间复杂度和O(1)的空间复杂度，但是会损坏链表
以下两个方法都是discuss比较好的
a) 非递归：龟兔赛跑，乌龟等着被兔子套圈
b) 递归：把每一个节点都连回自己，最后看有没有两个节点互相连。也会损坏链表

33. 在一个旋转过的数组里找到最小值(LeetCode153, medium)
基本算法和33相同，O(LgN)时间。话说为什么数组变成列表了。。。

34. M*N的矩阵，求一条最小和路径，只能向右向下。(LeetCode64, medium)
最基本的动态规划问题。可以优化到O(N)空间复杂度

35. 找出一组数里那个单蹦的（其他都是两个）(LeetCode163, medium)
神乎其技的位操作。。。解释在源码里

36. 三角形矩阵，求一条最小和路径，只能向下。(LeetCode120, medium)
最基本的动态规划问题。可以优化到O(N)空间复杂度。另外好像应该从底向上，这样就不用考虑边际条件
上到下一定要倒着枚举每一层。

37. 产生含有n个合法括号的全排列(LeetCode22, medium)
用最蠢的回溯方法做的（居然时间不是太烂）。。。别人的好回溯方法放在code里了，很好理解。

38. 输出给定序列的下一个排列（LeetCode31, medium）
三步走：找到第一个比它之前元素小的元素M；从元素M的右边搜索大于M-1的最小元素，交换这两个元素；倒转元素M到最后的所有元素；

39. 二分搜索元素的range(LeetCode33, medium)
先找到元素，再在元素两边继续二分查找，直到返回-1为止。但是应该是O(lgN*lgN)的时间复杂度
另外一个更好的算法在源码里

40. 手机按键全排列。(LeetCode17, medium)
我还是用的基本的递归回溯全排列。有一个非常漂亮的FIFO队列算法（好像是做了BFS）在源码里

41. partition一个链表(LeetCode86, medium)
分开两条链一大一小最后再连起来。

42. 求一个字符串的最长连续回文字串(LeetCode5, medium)
有三种流行的方法
a)动态规划，状态转移方程：P[i,j]{=P[i+1,j-1],if(s[i]==s[j])   =0 ,if(s[i]!=s[j])}
b)中心开花，时间复杂度同a相同，要对奇数和偶数分别做
c)Manacher法。真心没有看懂。。。

43. 列出一个字符串数组里所有字母相同但顺序颠倒的字符串(LeetCode49)
哈哈哈哈哈跑赢大盘了终于！这次我的方法时间复杂度O(M*N),同时discuss里都是O(M*N*LgN)。区别在于他们用sort，我直接hash。不过因为一共只有26个字母，可以用计数排序把排序算法的复杂度降到O(M*N)
hash的方法是给每个字符分配一个质数，hash值就是这些质数相乘。

44. 给一个矩阵，螺旋输出它的元素(LeetCode54, medium)
没什么难度，注意边界条件。

45. 合并一些区间。(LeetCode56, hard)
基本算法都是先排序，再合并。比较快的算法都是直接重写了Collection.sort()。有一点要注意，写CompareTo的时候一定不能违反了那四个contract，否则会抛异常。

46. 正则表达式匹配，支持.和*(LeetCode10, hard)
基本上是用的NFA正则引擎的思想写的，代码里有比较详细的解释

47. 最大盛水容器。(LeetCode11, medium)
跑平大盘！这次想出来的算法基本就是最优的：两个指针一头一尾，先计算当前容量，再看哪边小，小的地方指针前进（根据短板效应，小的地方最大值就是当前值，所以不需要继续查了，直接略过即可）

48. 验证一棵搜索二叉树。(leetCode98, medium)
前序遍历然后检查数组是否有序。50题里程碑！

49. 把一个排好序的数组转成平衡二叉搜索树(LeetCode108, medium)
没啥可说的，基础题。

50. 计算所有从根到叶子所组成的数的和(LeetCode129, medium)
还是很基本的题，递归搞定

51. 去除链表里所有重复的元素(LeetCode82, medium)
还是很基本的题，while跳过所有重复元素即可。递归做法放在了源代码里

52. 去除重复元素，如果有重复，保存两个。(LeetCode80, medium)
找到重复元素就复制两次，否则复制一次。就这么简单。

53. 把一个字符串还原成可能的IP地址(LeetCode93, medium)
先用回溯找四个数，每个数在1和3之间，加起来等于字符串长度。然后看着割开，一个一个检验就好。01这种直接抛弃

54. 判断一个字符串是不是合法的数字(LeetCode65, hard)
这题简直就是个噩梦。。。用了五个正则才解决，提交了20+次。。。

55. 给一个字母矩阵，判断想搜索的字符串是否在其中。(LeetCode79, medium)
DFS对每一个位置都过一遍即可。

56. 给一组数，判断怎么连接能让连成的数最大(LeetCode179, medium)
复习了一遍comparator的写法。。。就是两个字符串连起来比较就好了。壮哉我大Java

57. Unix风格匹配。(LeetCode44, hard)
这个题我一开始的思路就错了，不能用NFA去匹配，一定超时。
因为星可以匹配任何字符序列，所以应该是不管前面有多少星，只要当前不匹配，就要靠之前的星把位置顶上来。只要能匹配，总是能顶到正确的位置。

58. 给定n，输出一个旋转矩阵(LeetCode59, medium)
这题太简单了，代码抄下54就搞定了。。。

59. 对一个逆波兰表达式求值(LeetCode150, medium)
感觉难度不值medium。。。如果中波兰转逆波兰还是可以medium的

60. 找出一组数里那个单蹦的（其他都是三个）(LeetCode137, medium)
我的方法：过一遍加总，过一遍set加总，再过一遍，看看sum减掉哪个数正好是noDupSum减掉那个数的三倍，注意0的特殊情况
神的方法：使用状态机的位运算。。。

61. 给一组排好序的不重叠区间，插入一个新区间(LeetCode57, medium)
先在end里二分搜索新区间begin，再反过来搜索。确定区间以后用新的替换就好了，时间主要取决与传进来的是个什么List。
目测是个ArrayList，那我这个算法时间复杂度要到O(N^2)了。。。

62. 非递归后序遍历一颗二叉树(LeetCode145, hard)
我的方法能遍历，但是等于把树给拆了。。。discuss里头有个好方法：以根右左的顺序遍历二叉树，把结果倒过来输出。真是鸡汁啊！
第一种思路：对于任一结点P，将其入栈，然后沿其左子树一直往下搜索，直到搜索到没有左孩子的结点，此时该结点出现在栈顶，但是此时不能将其出栈并访问，因此其右孩子还为被访问。所以接下来按照相同的规则对其右子树进行相同的处理，当访问完其右孩子时，该结点又出现在栈顶，此时可以将其出栈并访问。这样就保证了正确的访问顺序。可以看出，在这个过程中，每个结点都两次出现在栈顶，只有在第二次出现在栈顶时，才能访问它。因此需要多设置一个变量标识该结点是否是第一次出现在栈顶。
第二种思路：要保证根结点在左孩子和右孩子访问之后才能访问，因此对于任一结点P，先将其入栈。如果P不存在左孩子和右孩子，则可以直接访问它；或者P存在左孩子或者右孩子，但是其左孩子和右孩子都已被访问过了，则同样可以直接访问该结点。若非上述两种情况，则将P的右孩子和左孩子依次入栈，这样就保证了每次取栈顶元素的时候，左孩子在右孩子前面被访问，左孩子和右孩子都在根结点前面被访问。

63. 非递归前序遍历一颗二叉树(LeetCode144, medium)
一个栈，重复弹栈顶元素-->右子树入栈-->左子树入栈这个过程就行了

64. 非递归中序遍历一颗二叉树(LeetCode144, medium)
1)若其左孩子不为空，则将P入栈并将P的左孩子置为当前的P，然后对当前结点P再进行相同的处理；
2)若其左孩子为空，则取栈顶元素并进行出栈操作，访问该栈顶结点，然后将当前的P置为栈顶结点的右孩子；
3)直到P为NULL并且栈为空则遍历结束

65. 求小于n的素数值
用筛法即可。辅以bitset食用更佳。

66. 返回一棵树的右视图(LeetCode199, medium)
DFS，每次加最后一个节点即可。

67. 计算两个字符串的编辑距离(LeetCode72, hard)
编辑距离（Edit Distance），又称Levenshtein距离，是指两个字串之间，由一个转成另一个所需的最少编辑操作次数。许可的编辑操作包括将一个字符替换成另一个字符，插入一个字符，删除一个字符。
用动态规划，如果a[i]==b[j]则直接过，不然就应该计算删除/添加/替换的最小值+1

68. 颠倒句子里单词(LeetCode151, medium)
先split，再reverse，最后join

69. 给一个target，计算数的路径和等于target的路径(LeetCode113, medium)
一层一层的递归即可，路上要记录节点

70. 找到小岛(LeetCode200, medium)
遍历一遍迷宫，遇到1就DFS把所有的岛都标记一遍，count++.

71. 打印两个整数相除的结果，标记循环节(LeetCode166, medium)
一个list记住所有位数，一个hashmap记住所有被除数，被除数出现循环就跳出

72. 一个数组里有很多个0,1,2，给这个数组排序(LeetCode75, medium)
方法1：从头开始，碰到2就换到后面去，碰到0就换到前面去
方法2：先过一遍计数，再直接赋值

73. 输出两个字符串的积(LeetCode43, medium)
就是高精度乘法的字符串版

74. 求1-n有多少不一样的二叉树(LeetCode95, medium)
一个动态规划，1-n轮流做root，树的个数就是左子树几种乘以右子树几种

75. 求一个给定集合的子集(LeetCode78, Medium)
跑平大盘！用0到2^n-1的每一个数字做位运算，0就加这个元素，1就不加

76. 给定一个矩阵，如果某个元素是0，那么把这个元素的行列都设置成0(LeetCode73, medium)
方法1：O(M+N)空间，用hashSet保存所有行列，然后设置即可
方法2：O(1)空间，用每一行每一列的第一个元素存放整行整列的状态。如果某个元素为0，那么该行该列的第一个元素设置成0.第一列要额外处理。

77. 实现pow(x, n)(LeetCode50, medium)
假设n = 10 = 1010, 所以x^10 = x^8 * x^2。就是把幂分成x的2的m次方乘起来

78. 有一列数，找到一个缺失的正数(LeetCode41, hard)
O(N)时间 + O(1)空间的做法：如果a[i] = i,不动；否则a[i]和a[a[i]]交换

79. 给一个区间[A,B]，返回从A一直到B的所有数字的AND值
只能说我还没领悟到位操作的真谛。。。

80. 给一个Unix路径，简化它(LeetCode71, medium)
这个没啥可说的，split之后一个switch就解决了

81. m*n的矩阵，只能向右走向下走，求有多少条路(LeetCode62, medium)
高三排列组合题：C(m+n-2, m-1)

82. 吃子：把所有被围起来的O换成X(LeetCode130, medium)
跟island一个思路，BFS/DFS标记所有边上的O，最后把所有没有被标记过的O转成X。递归版的BFS和DFS都溢出了，只有非递归版的能跑

83. 计算组合(LeetCode77, medium)
就是基本的回溯

84. 把一个矩阵顺时针旋转90度(LeetCode48, medium)
方法一：一层一层的旋转
方法二：先水平轴对称，再在/这个对角线上轴对称

85. 将二叉树的每一个节点都与它的右邻居连在一起(leetCode116, Medium)
按层遍历，最后把节点连在一起就好了
诶，审题审错了。。。原来是常数空间。答案已经放在源代码里头了。

86. 在一个上下左右都排过序的矩阵里搜索一个数(LeetCode74, medium)
方法一：把matrix当成一个大sorted Array，搜索即可
方法二：先在列二分搜索决定target在哪一行，再在行直接二分搜索

87. m*n的矩阵，只能向右走向下走，中间有障碍物，求有多少条路(LeetCode63, medium)
改成动归，遇到障碍物就把当前格子设成0

88. 输出n位的灰码(LeetCode89, medium)
报警了，他们用公式作弊：i^i>>1
我还拿个栈和list倒来倒去的。。。

格雷码属于可靠性编码，是一种错误最小化的编码方式。因为，虽然自然二进制码可以直接由数/模转换器转换成模拟信号，但在某些情况，例如从十进制的3转换为4时二进制码的每一位都要变，能使数字电路产生很大的尖峰电流脉冲。而格雷码则没有这一缺点，它在相邻位间转换时，只有一位产生变化。它大大地减少了由一个状态到下一个状态时逻辑的混淆。由于这种编码相邻的两个码组之间只有一位不同，因而在用于方向的转角位移量－数字量的转换中，当方向的转角位移量发生微小变化（而可能引起数字量发生变化时，格雷码仅改变一位，这样与其它编码同时改变两位或多位的情况相比更为可靠，即可减少出错的可能性。

89. 全排列(LeetCode46, medium)
有递归和非递归两种方法。记住这句话：全排列就是从第一个数字起每个数分别与它后面的数字交换

90. 把给定字符串按给定的字典切分(LeetCode139, medium)
方法一：效率奇差，先给Set按字符串长度排序，再挨个匹配。。。不行，超时
方法二：DP。我的动归掌握的还是不好，总是没法只考虑一个阶段。。。A[i] = A[j] && wordDict.contains(s.substring(j, i))

91. (LeetCode91, medium)
A message containing letters from A-Z is being encoded to numbers using the following mapping:

'A' -> 1
'B' -> 2
...
'Z' -> 26
Given an encoded message containing digits, determine the total number of ways to decode it.

For example,
Given encoded message "12", it could be decoded as "AB" (1 2) or "L" (12).

The number of ways decoding "12" is 2.
比较基本的DP问题，如果当前只能单蹦，那就和上一个分割的一样；如果可以和上一个组合，那就上一个加上上个。0的情况分开讨论

92. 曲里拐弯得遍历一棵树(LeetCode103, medium)
曲里拐弯得BFS遍历就好

93. 树迭代器，要求next返回下一个最小元素(LeetCode173, medium)
其实就是把中序遍历拆开。

94. 给一个数组表示股票价格，求最大利润(LeetCode121, medium)
后面的元素跟前面的作差，然后求新数组的最大子序列和即可

95. 给一个数组，找到peak element(LeetCode162, medium)
二分搜索，要求不停地往高处，往大的元素方向走就好了

96. 今天冲关的只能拿easy凑数了。。。给一个数组里的数+1(LeetCode66, easy)
太简单不说了

97. 给一个数组表示股票价格，求最大利润，可买卖多次(LeetCode121, medium)
这个题是逗我的吗。。。easy都不够格诶

98. 飞升了！！！飞升了！！！(LeetCode171, easy)

99. 克隆一个无向图(LeetCode133, medium)
BFS+HashMap即可

100. 好长时间没刷了。。。找到一个没排序的数组里的第K大的数(LeetCode215, medium)
随机化快排的partition部分+递归。算法导论的选择算法

101. 找到一个未排序的数组里的最长连续整数数列(LeetCode, medium)
用hashmap，但是相邻的integer都用链表连起来，最后算链表长度

102. 计算一个完全二叉树的结点个数(LeetCode222, medium)
先复习一下完全二叉树的定义：
完全二叉树：除最后一层外，每一层上的节点数均达到最大值；在最后一层上只缺少右边的若干结点。
所以计算方法就是：先算最后一层以上的，按满二叉树算。加上最后一层从根开始一路向下的二分搜索即可。

103. 反转二叉树(LeetCode226, easy)
我就路过做一下

104. 整数转罗马(LeetCode12, easy)
就是打表

105. 用加和位运算模拟整数除(LeetCode29, easy) 
就是移位来模拟二进制除。要把除数和被除数都转成long才能做。

106. 判断一个数组里是否有重复元素(LeetCode217, easy)
HashSet 5分钟搞定

107. 判断一个数组里是否有重复元素，而且重复元素距离小于k(LeetCode219, easy)
HashMap 5分钟搞定。有一个更好的方法附在代码里了

108. 重新排序链表(LeetCode143, medium)
O(N)的空间复杂度，用栈实现的，不够好。O(1)的方法在源码里，龟兔赛跑的原理，再合并链表

109. 在数组里删除给定的元素(LeetCode27, easy)
太简单不说了

110. 写一个支持括号和加减法的计算器(LeetCode224, medium)
不用栈，碰到括号就递归。。。正规的写法在源代码里

111. 用队列实现栈(LeetCode225, medium)
我的pop和top都是O(N),discuss有个方法push是O(N), pop和top是O(1)，就是存的时候倒过来了，不错。

112. 写一个支持四则运算的计算器(LeetCode227, medium)
我的方法：如果是加减号，看看栈顶是不是加减号，是就做运算再push。如果是乘除号，看看栈顶是不是乘除号，是就做运算再push，否则直接push。如果是数字，看看栈顶是不是乘除号，是就做运算在push，否则直接push。最后从左到右算一遍。这法子不好。discuss里的好办法是乘除全做运算push，加减直接push。最后全加起来。代码附近去了。

113. 课程设计，实际上是求一个有向图有没有环(LeetCode207, medium)
两种主流方法：拓扑排序(找到入度为0的节点并删除，重复这个操作直到不能再删除，看看是否仍有节点没有删除)和DFS找环(从每一个节点出发进行DFS遍历，看看有没有走到true的环上)。对Java来说DFS太慢了，我就没看到用DFS AC这道题的。。。。

114. 计算n!后面有多少个0.(LeetCode127, easy)
其实就是计算0-n有多少个因子5，用递推式f(n) = n/5 + f(n/5)

115. 计算一个给定的0-1矩阵里的最大正方形1的面积(LeetCode221, medium)
动归的代码附进去了。我的方法时间和空间复杂度都是O(N^2)，用两个矩阵存横和纵元素各有多少个1在前面，然后遍历matrix，对每一个元素遍历它的对角线即可
P[0][j] = matrix[0][j] 
P[i][0] = matrix[i][0] 
For i > 0 and j > 0: if matrix[i][j] = 0, P[i][j] = 0; if matrix[i][j] = 1, P[i][j] = min(P[i - 1][j], P[i][j - 1], P[i - 1][j - 1]) + 1.

116. 把一个二叉树展平成链表(LeetCode114, medium)
先把右子树放到左子树最右边，再把左子树转到右子树，然后下降一层。循环即可

117. 一个排好序的有重复的数组被右移了，搜索一个数字(LeetCode84, medium)
在33题的基础上的第II的情况3，由减半改成-1，这样保证不会被重复元素影响

118. 删除排好序的链表里的重复元素(LeetCode83, easy)
太简单了不说了

119. 在链表里删除指定的元素(LeetCode203, easy)
先找到再删

120. 找到一棵排序二叉树里第k大的元素(LeetCode230, medium)
我的方法是看左子树有多少个节点，然后再跟k做比较决定去左子树还是右子树还是返回根。可以用记忆数组优化这样就不用重复计算
好一点的方法是找到最左边然后向上回溯，代码在源代码里。