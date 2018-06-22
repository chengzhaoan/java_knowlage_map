## String
### 传送门
深入理解Java中的String（https://www.cnblogs.com/xiaoxi/p/6036701.html）

### 关键字
final  value[] offset count  hash

### 关键方法




### 问题
1. String 是线程安全的么？
本身不可变所以安全，线程的不安全来源于对共享资源的访问，都是自己私有的就没问题了。
2. 类似依靠不可变性的线程处理有哪些？
   CopyOnWriteArrayList 需要的话复制走（还同步回来么？）
3. str+str 效率真的很低么？
   我们处理一直在变化的str操作使用StringBulider这样效率会更高，（深入理解jvm中说）在现代虚拟机变成字节码的过程中会进行一系列的优化，并不一定会按照原始代码来走，包括set get 不会去真的用函数处理。
4. 为什么hashCode相等还要equals()相等,不仅仅是String
```
int h;//开始是0 但hashCode 不会是0的。
for (int i = 0; i < value.length; i++) {
     h = 31 * h + val[i];
}
```
String 的hashCode算法，这种算法也是一种摘要算法(类似的md5 )，所以是有概率重复的，先比较摘要，如果这个摘要相等再详细比较每个字符，这是一种分层比较的方式吗，加快了速度。
