#python 类

##python 类数据属性
####python类数据属性只属于类本身，可以通过实例来调用，但是不能通过实例来修改。如果通过实例来修改类属性，则会新产生一个实例属性，屏蔽掉类属性。
    
	class Music(object):
		music_name = "class property."
		"""docstring for Music"""
		def __init__(self, name):
			self.name = name

		@classmethod
		def GetClsName( cls ):
			return Music.music_name

	mu = Music("instance property.")
	
	print Music.music_name   #result is 'class property'
	print mu.music_name      #result is 'class property'
	Music.music_name = "another name" 
	print Music.music_name   #result is 'another name'
	mu.music_name = 'instance property' 
	print mu.music_name      #result is 'instance property'

####类属性不能放置于__init__中，因为__init__生成类的实例。

##python 特殊类属性
####__name__类的名字

    Musci.__name__
    mu.__class__.__name__
    
####__doc__类的描述
####__bases__类的所有父类构成的元组
####__dict__类的属性
####__class__产生实例的类

##python 类的实例
####__init__为创建实例后第一个调用的方法。
####__new__没有搞明白
####__del__类似C++析构函数

####python 一个很奇怪的属性，类属性单个值不能通过实例来修改，但是字典类型却可以。
    class C(object):
	"""docstring for C"""
	version = 1.0
	dic = {'username':'wang'}

	print str(C.version) + " " + C.dic['username']
	c1 = C()
	print str(c1.version) + " " + c1.dic['username']
	c1.version = 2.0
	c1.dic['password'] = '1234'
	print str(C.version) + " " + C.dic['username'] + " " 	+ C.dic['password']

##python子类调用父类的方法

    class DirevedClass( BaseClass ):
    	def __init__( self, var1, var2, var3 ):
    		BaseClass.__init__( self, var1, var2 )
    		self.var3 = var3
    		
####子类所有的属性均可以来自于父类
    class Music(object):
	"""docstring for Music"""
	def __init__(self, name):
		self.name = name
		self.copyRight = False

	class PopMusic( Music ):
		"""docstring for PopMusic"""
		def __init__(self, name, copyRight, price ):
			Music.__init__( self, name )
			self.copyRight = copyRight
			self.price = price

	popMusic = PopMusic( "I belive.", True, 10 )
	print popMusic.name, popMusic.copyRight, popMusic.price


####子类调用父类方法的另外一种写法
    class PopMusic( Music ):
    	def __init__( self, name, copyRight, price ):
    		super( PopMusic, self ).__init__( name )
    		pass    	
    	
    	
##静态方法和类方法
####静态方法无法访问实例变量和类的变量，类方法无法访问实例变量，但是可以访问类变量。
    

class Music(object):
	hasCopyRight = True
	"""docstring for Music"""
	def __init__(self, name):
		self.name = name

	@staticmethod
	def prefixInfo():
		print "this is music."

	@classmethod
	def GetCopyRight(cls):
		return Music.hasCopyRight

	mu = Music( "california dream." )
	if ( True == mu.GetCopyRight() ):
		print "This song has copyright."
	else:
		print "This song is forbbiden to download."

	mu.prefixInfo()
	
##issubclass & isinstance

##类的hasattr(), getattr(), setattr(), delattr()
####到了比较关键的地方了，教程不是很详细啊
   hasattr() 是检测某个对象是否有一个特定的属性，getattr()在你试图读取一个不存在的属性时，引发一个AttributeError异常。setattr()如果属性不存在则创建，如果存在则修改。delattr()删除属性
   给个例子说明：
    
class Music(object):
	"""docstring for Music"""
	def __init__(self, name):
		self.name = name
		self.copyRight = False

	def GetName( self ):
		return self.name

	mu = Music( "agentina" )
	if True == hasattr( mu, 'GetName' ):
		print mu.GetName()

	if True != hasattr( mu, 'SetName' ):
		setattr( mu, 'type', 'pop' )

	print mu.type

	if True == hasattr( mu, 'type' ):
		delattr( mu, 'type' )

	print hasattr( mu, 'type' )
	
最终还是没有研究明白，如何用setattr来添加一个实例方法。

##python __getattribute__方法，指定属性不论是否存在都会被调用。而__getattr__在属性不存在时才会触发。



	