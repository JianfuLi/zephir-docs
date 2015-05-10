编译器警告
=================

当编译器发现有可以改善的代码或者可避免潜在的错误时，就会触发警告。

警告可以通过命令行参数来启用，也可以在config.json里开启或者禁用：
你可以用单词的前缀 -w 来启用它（小写）：

.. code-block:: bash

    zephir -wunused-variable -wnonexistent-function

禁用警告也是用单词的前缀 -W （大写）：

.. code-block:: bash

    zephir -Wunused-variable -Wnonexistent-function

Zephir支持以下警告

unused-variable
^^^^^^^^^^^^^^^
方法中已申明的变量未被使用时触发，访警告默认启用：

.. code-block:: zephir

    public function some()
    {
        var e; // declared but not used

        return false;
    }

unused-variable-external
^^^^^^^^^^^^^^^^^^^^^^^^
方法中已申明的参数未被使用时触发：

.. code-block:: zephir

    public function sum(a, b, c) // c is not used
    {
        return a + b;
    }

possible-wrong-parameter-undefined
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
调用方法时使用了错误的类型参数时触发：

.. code-block:: zephir

    public function some()
    {
        return this->sum("a string", "another");  // wrong parameters passed
    }

    public function sum(int a, int b)
    {
        return a + b;
    }

nonexistent-function
^^^^^^^^^^^^^^^^^^^^
在编译期间调用不存在的方法时触发：

.. code-block:: zephir

    public function some()
    {
        someFunction(); // someFunction does not exist
    }

nonexistent-class
^^^^^^^^^^^^^^^^^
在编译期间使用不存在的类时触发：

.. code-block:: zephir

    public function some()
    {
        var a;

        let a = new \MyClass(); // MyClass does not exist
    }

non-valid-isset
^^^^^^^^^^^^^^^
当编译器检测到isset操作应用于非数组或对象时触发：

.. code-block:: zephir

    public function some()
    {
        var b = 1.2;
        return isset b[0]; // variable integer 'b' used as array
    }

non-array-update
^^^^^^^^^^^^^^^^
当编译器检测到对非数组对象进行数组的更新操作时触发：

.. code-block:: zephir

    public function some()
    {
        var b = 1.2;
        let b[0] = true; // variable 'b' cannot be used as array
    }

non-valid-objectupdate
^^^^^^^^^^^^^^^^^^^^^^
当编译器检测到对非对象进行对象的更新操作时触发：

.. code-block:: zephir

    public function some()
    {
        var b = 1.2;
        let b->name = true; // variable 'b' cannot be used as object
    }

non-valid-fetch
^^^^^^^^^^^^^^^
当编译器检测到fetch操作作用于非数组或对象时触发：

.. code-block:: zephir

    public function some()
    {
        var b = 1.2, a;
        fetch a, b[0]; // variable integer 'b' used as array
    }

invalid-array-index
^^^^^^^^^^^^^^^^^^^
当编译器检测到无效的数组索引时触发：

.. code-block:: zephir

    public function some(var a)
    {
        var b = [];
        let a[b] = true;
    }

non-array-append
^^^^^^^^^^^^^^^^
当编译器检测到元素被追加到非数组变量时触发：

.. code-block:: zephir

    public function some()
    {
        var b = false;
        let b[] = "some value";
    }
