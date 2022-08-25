# 作用于函数

## 总结

* let 闭包中上下文仍然是对象本身，可以重新定义变量名称，也可以直接使用it；let闭包如果需要返回值，则需要显式使用 return。

![image](https://user-images.githubusercontent.com/6744261/186563699-6aac9921-824e-4867-a138-60e270104411.png)


* with 闭包中上下文也是这个对象，只不过默认是this，不用显式调用this，直接可以调用对象的方法，最后一行就是with闭包的返回值，不用显式使用 return。

![image](https://user-images.githubusercontent.com/6744261/186564862-fb54286a-1df3-425e-9c88-1ce626e85833.png)


* run 跟with十分类似，唯一不同就是在对象上调用，更符合使用习惯。

![image](https://user-images.githubusercontent.com/6744261/186565391-b5f349d0-7871-4b00-b821-38977cd97c95.png)

* apply 适合链式调用，默认返回对象本身，不用显式调用 return 返回对象本身，如果希望用另个对象进行后续的链式调用，则需要显式调用 return。

![image](https://user-images.githubusercontent.com/6744261/186567192-e04d716c-5cbc-4bd4-8e48-2713d8272397.png)


## let代码实例

```kotlin

class LetScope {

    /**
     * 有返回值let
     */
    fun testLet(name: String?): String? {
        return name?.let {
            println("hello: $it")
            return "welcome $it"
        }
    }

    /**
     * 无返回值let
     */
    fun testLet1(name: String?): String? {
        name?.let {
            println("hello: $it")
        }
        return null
    }

    /**
     * 自定义let参数
     */
    fun testLet2(name: String?): String? {
        name?.let { renameParam ->
            println("hello: $renameParam")
        }
        return null
    }
}

fun main() {
    val scope = LetScope()
    var result: String? = null

    /**
     * 测试有返回值let
     */
    result = scope.testLet("jack")
    println(result)

    /**
     * 测试无返回值let
     */
    result = scope.testLet1("jack")
    println(result)

    /**
     * 测试自定义参数（避免let嵌套，导致多个it混乱）
     */
    result = scope.testLet2("jack")
    println(result)
}

```


## with 代码示例

```kotlin

class WithScope {

    /**
     * 闭包最后一行就是闭包的返回值
     * 可以this显式调用，也可以省略
     */
    fun testWith(): String? {
        return with(StringBuilder()) {
            this.append("Hello")
            append(" ").append("world")
            toString()
        }
    }
}

fun main() {
    val scope = WithScope()
    var result: String? = null

    /**
     * 测试with
     */
    result = scope.testWith()
    println(result)
}

```

## run 调用示例

```kotlin

class RunScope {

    /**
     * 闭包最后一行就是闭包的返回值
     * 可以this显式调用，也可以省略
     */
    fun testRun(): String? {
        return StringBuilder().run {
            this.append("Hello")
            append(" ").append("world")
            toString()
        }
    }
}

fun main() {
    val scope = RunScope()
    var result: String? = null

    /**
     * 测试 run
     */
    result = scope.testRun()
    println(result)
}

```

## apply代码示例

```kotlin

class ApplyScope {

    /**
     * 1、不显示调用return，返回对象本身；
     * 2、也可以通过显示调用return，返回其他类型的话，就需要在其他类型上做链式调用
     * 可以this显式调用，也可以省略
     */
    fun testApply(): String? {
        return StringBuilder().apply {
            this.append("Hello")
            append(" ").append("world")
        }.toString()
    }
}

fun main() {
    val scope = ApplyScope()
    var result: String? = null

    /**
     * 测试 apply
     */
    result = scope.testApply()
    println(result)
}

```
