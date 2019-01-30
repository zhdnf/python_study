#### Unittest 和 Nose

一、 基本概念：python进行单元测试的框架

二、 Unittest模块内容

1. 基本代码

	``` class TestStringMethods(uniitest.TestCase):
		def test_upper(self):
			self.asserEqual('foo'.upper(). 'FOO')
	if __name__ == '__main__':
		unittest.main()```
2. setUp, tearDown
	- setUp 当测试开始前执行的操作
	- tearDown 当测试结束后执行的操作
	
	```class TestStringMethods(uniitest.TestCase):
		def setUp(self):
			print("123")
		def tearDown(self):
			print("456")
		def test_upper(self):
			self.asserEqual('foo'.upper(). 'FOO')
	if __name__ == '__main__':
		unittest.main()```
3. suite 可以添加任意的测试用例

	```suite = unittest.TestSuite()
	suite.addTest(TestStringMethods(test_upper))
	unittest.TextTestRunner().run(suite)```
4. skip, skipIf
	- skip @unittest.skip("xxx") 跳过下列修饰的测试用例
	- skipIf @unittest.skipIf(condition,"xxx") 满足条件跳过下列修饰的测试用例

5. 断言
	- assertEqual(a, b)  a==b 
	- assertTrue(x)    bool(x) is True
 	- assertIs(a, b)   a is b
    - 剩余请看官方文档

三、 unittest.mock 模块内容
1. mock: 用一个虚拟的对象(mock)来创建以便测试的测试方法

2. mock方法
	- assert_called_with(*args, **kwargs) 当前对象是否被调用
	- assert_called_once_with(*args, **kwargs) 对象是否调用大于1次
	- assert_any_call(*args, **kwargs) 是否被调用过
	- assert_has_calls(calls, any_order=False) 是否按照有顺序的调用列表调用
	- reset_mock() 重置当前的mock对象
3. mock属性
	- called 是否被调用(返回值True or False)
	- call_count 被调用的次数
	- return_value 调用mock的返回值
	- side_effect 也是mock的返回值，优先级大于return_value，可以取iter对象
4. patch 通过patch使用自己的名字来使用其他模块的对象

（```@patch('module.ClassName2')
		@patch('module.CalssName1')
		def test(MockClass1, MockClass2):
			module.ClassName1()
			module.ClassName2()
			assert MockClass1 is module.ClassName1
			assert MockClass2 is module.ClassName2
		test()```)
		
四、 Nose 也是python的自动化测试框架，但unittest不支持参数化测试，Nose支持

1. parameterized
	使用nosetests执行py程序

    (```@parameterized([
			(2, 2, 4),
			(2, 3, 8),
			(1, 9, 1),
			(0, 9, 0),
		])
		def test_pow(base, exponent, expected):
			assert_equal(math.pow(base, exponent), expected)
		class TestMathUnitTest(unittest.TestCase):
			@parameterized.expand([
				("negative", -1.5, -2.0),
				("integer", 1, 1.0),
				("large fraction", 1.6, 1),
			])
			def test_floor(self, name, input, expected):
				assert_equal(math.floor(input), expected)```)
		
五、 官方文档

1. unittest：https://docs.python.org/2/library/unittest.html
2. unittest.mock：https://docs.python.org/3.4/library/unittest.mock.html#patching-descriptors-and-proxy-objects
