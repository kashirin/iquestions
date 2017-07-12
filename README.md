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

