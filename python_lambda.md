#python lambda

####python的lambda表达式也就是匿名函数，冒号前面为输入参数，冒号后面为需要返回的表达式

    func = lambda x : x * x
    func( 4 )
    
    result is 4
    
#python filter

####python的filter内置函数，入参第一个为函数表达式，类似C的函数指针，第二个参数为数据值。filter类似滤网。

    print filter( lambda x : x * x, range( 1, 10 ) )
    
    result is 4, 5, 6, 7, 8, 9
    
#python map

####python的map内置函数，它将函数关系映射到每一个序列元素上，并返回所有返回值的列表。

    print map( lambda x : x * x, range( 1, 3 ) )
    result is 1,4,9
    print map( lambda x, y : x * y, [1,2,3], [4,5,6])
    result is []4,10,18]
    
    
####python的map可以实现和zip内置函数一样的效果。

    print map( None, [1,2,3,4],[4,5,6,7] )
    result is [(1,4),(2,5),(3,6),(4,7)]
    print zip([1,2,3,4],[4,5,6,7])
    
#python reduce

####python的reduce内置函数将一个序列的值逐个以函数操作，遍历。

    print reduce( lambda x, y : x + y, range(1,10))
    the result is 45
    print reduce( lambda x, y : x * ( y + 1 ), range( 1, 5) )
    the result is 60
    
#python partial

####partial用来产生偏函数应用PFA

    from functools import partial
    def fun( var1, var2 ):
    	return var1 * var2
    
    for i in range( 1, 10 ):
    	partial( fun, i )( 100 )
    	
#python 闭包
####闭包指的是某函数包含的变量，具有自己的作用域。

    def counter( start_at = 0 ):
	count = [start_at]
	def incr():
		count[0] += 1
		return count[0]

	return incr

	count = counter(5)
	print count()   6
	print count()   7
	print count()   8

####高级一点的例子如下：
    from time import time

	def logged( when ):
		def log( f, *args, **kargs ):
			print '''called:
				function: %s
				args: %r
				kargs: %r''' %( f, args, kargs )

	def pre_logged(f):
		def wrapper(*args, **kargs):
			log( f, *args, **kargs )
			return f( *args, **kargs )

		return wrapper

	def post_logged(f):
		def wrapper( *args, **kargs ):
			now = time()
			try:
				return f(*args, **kargs )
			finally:
				log( f, *args, **kargs )
				print "time delta: %s" %(time() -now)

		return wrapper

	try:
		return {"pre": pre_logged, 
		"post": post_logged}[when]
	except KeyError, e:
		raise ValueError( e ), 'must be "pre" or "post"'


	@logged("post")
	def Hello(name):
		print "hello", name


	Hello( "World!" )
	
#python递归
####经典的例子就是阶乘
    def factorial( n ):
    	if n == 0 or n == 1:
    		return 1
    	else:
    		return ( n * factorial( n - 1 ) )
