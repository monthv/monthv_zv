JavaScript

1、简单闭包
var scope="可能";

function ManScope(){
	var scope="或者";
  function Man(){
  		return scope;
  }
  return Man();
}
ManScope();
//执行后输出：或者
