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
	
	$f2 = new Foo2();
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

## Question 2

Consider the following php code:
```
class DoSome {

	protected $_type;

	public function __construct($whatType){
		$this->_type = $whatType;
	}
	
	protected function doFirst(){
		// some code
		// ...
		if($this->_type == 'typeA'){
			//...do A algo
		}else if($this->_type == 'typeB'){
			//...do B algo
		}
	}
	
	protected function doSecond(){
		// some more code
		//...
		if($this->_type == 'typeA'){
			//...do A algo
		}else if($this->_type == 'typeB'){
			//...do B algo
		}
	}
	
	public function doFinally(){
		// common code
		// ...
		if($this->_type == 'typeA'){
			//...do A algo
			//... some more for A
			//...
			// then
			$this->doFirst();
			$this->doSecond();
			// finaly do for A
		}else if($this->_type == 'typeB'){
			//...do B algo
			//... some more for B
			//...
			$this->doFirst();
			$this->doSecond();
			// finaly do for B
		}
	}

}

$item = new DoSome('typeA');
$item->doFinally();
$item = new DoSome(‘typeB’);
$item->doFinally();
```
What is the problem with this code? How we can enhance it?

## Question 3

Consider the following php code:

```
class ROOT {
     protected function a()
     {
         print_r(get_class($this).': from protected base class ⟨br⟩');
     }
 }

class CHILD2 extends ROOT{

} 

class CHILD extends ROOT {

     public function b()
     {
         $ss = new CHILD2();
         $ss->a();
     }
 }
 

$a = new CHILD();
$a->b();
```
Will this code work? What will be printed on screen if we run it?

## Question 4

Consider the following php code:

```
class Foo{
	
	protected $state = null;
	protected $level = null;
	
	public function setState($state){
		$this->state = $state;
	}
	public function setLevel($level){
		$this->level = $level;
	}
	
	//...more methods and props
	
	public function report(){
		echo 'State is ['.$this->state.'], level is ['.$this->level.']';
	}
	
}

$f = new Foo();

$f->setState('empty');
$f->setLevel('5');
$f->report();
```

Supposed we have very long class Foo. It has dozen different boring methods and properties. In order to debug code right here and right now we need some modification of class Foo to provide logging each method invocation. Suppose we want to catch in log only two moments - just before method will be invoked and right after it will finished own work. For the first case we want to catch method name and passed arguments. For the second - only method name. Below the example output you need to obtain:
