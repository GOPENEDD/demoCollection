在读写流的时候，都是以自己为主体
intput，流向自己写入，就是读取流。read
output，我们向流输出，就是写入流，write

###一个下载任务一个线程
1. 根据url生成文件名以及文件路径
1. 读取本地的文件大小，作为range的参数
   在http头里面，Range：0-100 表示这次请求需要返回的文件是0到100字节
   http的返回头里会有content-length表示内容的大小，Content-Range返回的是这次的范围，如果请求的range超过了，Content-Range就是空了
   本地文件大小为0的时候，Range：0-     表示请求全部
   暂停后再请求：Range：1000-  表示请求从1000开始
   当文件下载完成后，假设文件大小为10000字节，再请求 10000-    这时候Content-Range会返回空，而我们也不做写入操作了
   http头有Range的时候返回206

###一个下载任务多个线程




java中int是32位 最大2147483647 折算成GB约等于1.9GB ,所以只下载小文件的话int还是控制的住的