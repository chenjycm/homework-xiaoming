# Thoughtworks校园招聘作业ReadMe
------

> * 作者：陈建名
> * 学校：北京邮电大学
> * 专业：信息管理与信息系统（本）、管理科学与工程（信息化与信息技术方向/硕）

##一、程序介绍
> * 编程语言：JavaScript
> * 编程工具：Sublime text 2
> * 文件类型：Html（JavaScript程序已写入Html）
> * 输出及测试：通过Chrome浏览器进行输出，通过console语句对每个函数的功能及正确性进行测试，在Chrome控制台console项下查看测试结果。
> * Readme说明：采用Markdown排版

##二、使用说明

 1. 通过浏览器运行index.html，建议采用Chrome浏览器打开。
 2. 在网页页面左边给出数据的示例，一行数据的格式为{活动时间 yyyy-MM-dd HH:mm~HH:mm}{人数}，若有多条数据，使用回车换行。
 3. 按照要求的格式在页面中间上部的输入框中输入数据，也可将示例数据直接复制粘贴到输入框中。
 4. 点击“计算”按钮，输出结果将会在下部的输出框中显示；若要清除输入框及输出框中的文本，请点击“清除”。
 
##三、JavaScript函数说明
本JavaScript程序中包含7个函数，其中前面六个为计算函数，最后一个为读取和输出函数，如下表：

| 函数名       | 功能   |
| --------   | :-----  | 
|comp_day (day){}| 通过打球日期计算该日期的星期数|  
|comp_cost(day,time){}|   通过打球时期和打球时间，计算每个场地每小时的费用|
|comp_court (people){}| 通过打球人数，计算预定的场地数量 |
|get_money(people){} |通过报名人数，计算每次打球活动的收入|
|cost_money(day,time,people){}|通过日期、时间和人数，计算每次打球活动的支出|
|earn_money(day,time,people){}|通过日期、时间和人数，计算每次打球活动的盈余|
|in_out(){}|读取输入的数据，并输出计算结果|

###1、函数：comp_day(day){}
通过打球日期计算该日期的星期数，参数day的格式为{yyyy-MM-dd}，通过调用Date对象和getDay()方法，获得0至6的数，0表示星期天、1表示星期一、2表示星期二以此类推。通过console.log在控制台输出结果，验证函数的有效性，代码如下:
```JavaScript
function comp_day (day){    //根据日期计算星期数，星期天为0，星期一为1，星期二为2，以此类推。
    var a=new Date(day); 
    return a.getDay(); 
}   
console.log(comp_day("2016-06-06"));
```
 ###2、函数：comp_cost(day,time){}
 通过日期和时间，计算该日该时每个场地每个小时的费用。
（1）先通过将时间{1200~15:00}通过.split按照“~”符号进行拆分，并赋值给数组timeline,其中timeline的第一个元素表示开始时间{12:00}，第二个元素表示结束时间{15:00}，在通过.split按照“:”将时间拆分成文本{12、15}，将数字文本转化为整型数据，这样可以获得小时的数字s1和f1。
（2）通过for循环嵌套if语句，计算开始时间s1所在星期和时间段每个场地的费用，以开始时间s1和结束时间f1的大小比较作为循环跳出判断，每次循环通过p进行累加计算出每个场地每次活动的费用。
（3）通过console.log对费用p进行输出测试。
```JavaScript
function comp_cost(day,time){   
    var timeline = time.split("~");
    var start_time = timeline[0].split(":");
    var finish_time = timeline[1].split(":");       var s1 = parseInt(start_time[0]);
    var f1 = parseInt(finish_time[0]);  
    console.log("开始时间："+s1);
    console.log("结束时间："+f1);
    var fee = 0; var p = 0;        //fee表示单位场地每个小时的费用，p表示每个场地在不同时间费用合计 
    var days = comp_day(day);       //调用计算星期的函数，把日期转化为星期数
    for(s1;s1<f1;s1++){
       if(days>0&&days<6){
       if(s1<12){fee = 30;}
       	else if(s1<18) {fee=50;}
       	else if(s1<20) {fee=80;}
       	else {fee=60;}
       }else{
       	  if(s1<12) {fee=40;}
       	  else if(s1<18) {fee=50;}
       	  else {fee=60;}
       	  }
       p+=fee;	
     }
    return p; 
} 			
console.log("星期"+comp_day("2016-06-06"));
console.log("每个场地活动费："+comp_cost(comp_day ("2016-06-06"),"12:00~15:00"));  
```
###3、函数：comp_court(people){}。
通过报名人数，计算需要预定的场地数量。
（1）将人数作为输入，t表示可以立即确定的场数，x表示需要判断的多余人数。
（2）根据t、x和订场策略，利用if语句进行策略选择，最后获得需要预定的订场数量court。
```JavaScript
function comp_court (people){
    var t=parseInt(people/6);  
    var x=people%6;
    var court = 0;
      if(t==0&&x<4) { court=0; } 
      else if(t==0&&x>=4){court=1;}
      else if(t==1) {court=2;}
      else if((t==2||t==3)&&x<4) {court=t;}
      else if((t==2||t==3)&&x>=4) {court=t+1;}
      else if(t>3) {court=t;}
      return court;
} 
 console.log("预定场地数："+comp_court(15));
```
###4、函数：get_money(people){}
通过报名人数，计算每次打球活动的收入。收入=参与活动的人数*30。若人数小于4，活动取消。
```JavaScript
function get_money(people){  //计算每次的收入。
    var a = 0;
    if(parseInt(people)<4){a=0;}
    else {a = parseInt(people)*30;}
    return a;
} 
```
###5、函数：cost_money(day,time,people){}
计算每次的活动的总费用，总费用=每个场地的费用*场地数量。
```JavaScript
function cost_money(day,time,people) {      //计算每次的总费用：每个场地的费用*场地数量。
    var b = comp_cost(day,time)*comp_court(people);
    return b;
} 
console.log("每个场地费："+comp_cost("2016-06-03","09:00~12:00")+" 场地数："+comp_court(14));  
```
###6、函数：earn_money(day,time,people){}
通过日期、时间和人数，计算每次打球活动的盈余资金。盈余=总收入-总支出。
```JavaScript
function earn_money(day,time,people){         //计算盈余的资金。
    var e = get_money(people)-cost_money(day,time,people);
    return e;
}    
```
###7、函数：get_data(){}
读取输入框中的数据，并返回一个对象数组。
（1）通过document.getElementById("list").value获得文本框的中的数据存入变量catch_text（只有一个文本包含所有数据 ），通过split根据换行符对数据进行拆分，存入数组lists（每个元素只有一个值：yyyy-MM-dd HH:mm~HH:mm），再通过for循环对每个lists的值进行拆分，得到对象数据each_t。
```JavaScript
 function get_data(){
	var catch_text = document.getElementById("list").value;  
    var lists = catch_text.split("\n");   	 // lists表示输入的打球信息
    console.log("活动信息读入："+"\n"+catch_text);   
    console.log("打球次数:"+lists.length+"次");
	var each_t = new Array();   //存储每次活动的情况，
    for(var i=0;i<lists.length;i++){       //将每行输入的数据存在对象each_time中，其每个元素有三个属性，分别是日期、时间和人数 。     		
    each_t.push(lists[i].split(" "));
     }
    return each_t;
}
```
###8、deals(option){}
对获取的数据进行处理，将原来只有三个属性值的对象，转化为具有五个属性值的对象，并返回。调用get_money(),cost_money(),earn_money(),计算收入、支出和盈余，并存入option对象中。
```JavaScript
function deals(option){
    var days = option[0];
    var times =option[1];
    var get_s ;                           //给需要输出的
    var cost_s ;
    var earn_s ;	
    if (get_money(option[2])>0) {      // if语句对收入、支出和盈余的数据添加“+”或者“-”
      get_s = "+"+get_money(option[2]);
      }else{
      get_s="-"+get_money(option[2]);}	        		
    cost_s="-"+cost_money(option[0],option[1],option[2]); 
    if(earn_money(option[0],option[1],option[2])>0){
        			earn_s = "+"+earn_money(option[0],option[1],option[2]);
        		} else {earn_s = earn_money(option[0],option[1],option[2]);}
        	    var t = {day:days,time:times,getMoney:get_s,costMoney:cost_s,earnMoney:earn_s};  
    return t;//将五个属性数据临时存入tmp对象中        	}
```
###9、in_out()
输入输出函数。
（1）开始通过获取输入框的值是否存在，对用户输入进行提示；
（2）调用读取数据的函数get_data()获取经过一定处理的数据，利用for循环对读取的数据按照要求进行添加“+”和“-”的处理，
（3）按照要求格式输出数据
```JavaScript
function in_out(){           //数据读入和结果输出
    if(document.getElementById("list").value.length == 0 ){ 
    alert("无数据输入，请重新输入！");
    } else{
     document.getElementById('box').innerHTML = document.getElementById('box').innerHTML+"</br>"+"[Summary]"+"</br>";           //输出标题
     var each_time = get_data();
     var a = each_time.length;  console.log("测试次数："+a);
     var sum = new Array();        //构建对象数组，每个对象中存储每次的计算汇总数据。
     var total_In = 0;
     var total_Pay = 0;
     var profit = 0;
     for(var i=0; i<a ;i++){        //将经过计算并处理后的没行数据存入sum对象中，其每个元素包括5个属性，分别为	日期、时间、收入、支出和盈余。
      x = each_time[i];
      var tmp = deals(x);
      sum.push(tmp);      //将tmp对象数据push到sum数组
      total_In+=get_money(x[2]);      //计算收入、支出和盈余
      total_Pay+=cost_money(x[0],x[1],x[2]);
      profit+=earn_money(x[0],x[1],x[2]);
      document.getElementById('box').innerHTML = document.getElementById('box').innerHTML+"</br>"+sum[i].day+" "+sum[i].time+" "+sum[i].getMoney+" "+sum[i].costMoney+" "+sum[i].earnMoney;
      }
    document.getElementById('box').innerHTML = document.getElementById('box').innerHTML+ "</br>" + "</br>"+"Total Income: "+total_In+"</br>"+"Total Payment: "+total_Pay+"</br>"+"Profit: "+profit+"</br> ";
    }
}
```
###10、函数：clear_text(){}。
通过调用函数清除输入框和输出框中的内容，以便于重新输入和计算。
```JavaScript
function clear_text(){
   	console.log("内容清除程序调用成功！");
   	document.getElementById('list').value="";
   	document.getElementById('box').innerHTML="";
}
```
 
##四、优点与不足
优点：本程序采用JavaScript语言，利用Chrome浏览器进行测试和展示，较为方便。

不足：由于展示和理清思路的需要，一些地方并没有完全简化，时间有限，还有许多需要改进或简化的地方。