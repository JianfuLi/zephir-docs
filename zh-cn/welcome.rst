欢迎!
========
欢迎来到Zephir，这是一个开源、高级的领域特定语言，它能很容易的创建和维护PHP扩展，重点是类型系统和内存操作是安全的。

主要功能
-------------
Zephir主要的功能有：

+-------------------+-----------------------------------------------------+
| 类型系统          | 动态/静态                                           |
+-------------------+-----------------------------------------------------+
| 内存安全          | 不允许使用指针或直接内存管理                        |
+-------------------+-----------------------------------------------------+
| 编译模型          | 事前编译（也叫静态编译）                            |
+-------------------+-----------------------------------------------------+
| 内存模型          | task-local garbage collection                       |
+-------------------+-----------------------------------------------------+

一个小例子
-------------
下面的代码注册了一个Filter类，Filter类的alpha方法返回给定参数的字母

.. code-block:: zephir

    namespace MyLibrary;

    /**
     * Filter
     */
    class Filter
    {
        /**
         * Filters a string returning its alpha characters
         *
         * @param string str
         */
        public function alpha(string str)
        {
            char ch; string filtered = "";

            for ch in str {
               if (ch >= 'a' && ch <= 'z') || (ch >= 'A' && ch <= 'Z') {
                  let filtered .= ch;
               }
            }

            return filtered;
        }
    }

在PHP中使用这个类：

.. code-block:: php

  <?php

  $filter = new MyLibrary\Filter();
  echo $filter->alpha("01he#l.lo?/1"); // prints hello
