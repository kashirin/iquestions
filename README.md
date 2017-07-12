# Interview Questions

## Question 1

Consider the following php code:
```
abstract class Foo{
		abstract protected function doSomeWith($data);
		
		abstract protected function doSomeMore();
		
		abstract protected function doAnotherThings($data);
		
		public function needPrepare($data){
			...
			$this->doAnotherThings($data);
			...
			$this->doSomeWith($data);
			...
		}
		
		public function run($data){
			...
			$this->doSomeWith($data);
			...
			$this->doSomeMore();
			...
		}
	}
	
	class Foo1 extends Foo{
		protected function doSomeWith($data){
			...
		}
		
		protected function doSomeMore(){
			...
		}
		
		protected function doAnotherThings($data){
			...
		}
	}
	
	class Foo2 extends Foo{
		protected function doSomeWith($data){
			...
		}
		
		protected function doSomeMore(){
			...
		}
		
		protected function doAnotherThings($data){
			...
		}
	}
	
	$f1 = new Foo1();
	$f1->run('one');
	
	$f2= new Foo2();
	$f2->needPrepare('some data');
	$f2->run('two');
```
You need to modify this code in that way: every protected methods of each descendant class must write some text to a log-file. Restriction: you cannot modify any descendant class. Supposed we have log function with name `log`. Below the example output you need to obtain:
```
a piece of result log-file
	method Foo1->doSomeWith called with data: 'one'
	before calling method Foo1->doSomeMore;
	after calling method Foo1->doSomeMore;
	
	method Foo2->doAnotherThings with data: 'some data'
	method Foo2->doSomeWith called with data: 'some data'
	method Foo2->doSomeWith called with data: 'two'
	before calling method Foo2->doSomeMore;
	after calling method Foo2->doSomeMore;
```

