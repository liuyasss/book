##　ArrayMap　&&　HashMap 

#### 差异:

1. 存储方式不同：ArrayMap内部使用两个数组，一个存HashCode，一个存键值对对象。HashMap内部是Entry对象
2. 扩容方式不同：上面HashMap源码分析这篇文章说过了，HashMap初始大小是16，达到满容量的0.75时，要扩容，每次都是上次容量的2倍



### 总结:

> ArrayMap在内存使用率上比HashMap高不少，但是插入速度在数据很多时会很慢，所以ArrayMap在数据量少时（千以内）比较适用，否则还是要使用HashMap。

> 1.在数据量小的时候一般认为1000以下，当你的key为int的时候，使用SparseArray确实是一个很不错的选择，内存大概能节省30%，相比用HashMap，因为它key值不需要装箱，所以时间性能平均来看也优于HashMap,建议使用！
> 2.ArrayMap相对于SparseArray，特点就是key值类型不受限，任何情况下都可以取代HashMap,但是通过研究和测试发现，ArrayMap的内存节省并不明显，也就在10%左右，但是时间性能确是最差的，当然了，1000以内的数据量也无所谓了，加上它只有在API>=19才可以使用，个人建议没必要使用！还不如用HashMap放心。估计这也是为什么我们再new一个HashMap的时候google也没有提示让我们使用的原因吧。