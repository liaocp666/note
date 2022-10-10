String 是不可变的，尝试去修改，会生成一个新的字符串对象，StringBuffer 和 String Builder 是可变的。

String Buffer 是线程安全的，String Builder 是线程不安全的。在单线程下 String Builder 效率高。