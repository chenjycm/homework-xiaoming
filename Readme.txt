# ThoughtworksУ԰��Ƹ��ҵReadMe
------

> * ���ߣ��½���
> * ѧУ�������ʵ��ѧ
> * רҵ����Ϣ��������Ϣϵͳ�������������ѧ�빤�̣���Ϣ������Ϣ��������/˶��

##һ���������
> * ������ԣ�JavaScript
> * ��̹��ߣ�Sublime text 2
> * �ļ����ͣ�Html��JavaScript������д��Html��
> * ��������ԣ�ͨ��Chrome��������������ͨ��console����ÿ�������Ĺ��ܼ���ȷ�Խ��в��ԣ���Chrome����̨console���²鿴���Խ����
> * Readme˵��������Markdown�Ű�

##����ʹ��˵��

 1. ͨ�����������index.html���������Chrome������򿪡�
 2. ����ҳҳ����߸������ݵ�ʾ����һ�����ݵĸ�ʽΪ{�ʱ�� yyyy-MM-dd HH:mm~HH:mm}{����}�����ж������ݣ�ʹ�ûس����С�
 3. ����Ҫ��ĸ�ʽ��ҳ���м��ϲ�����������������ݣ�Ҳ�ɽ�ʾ������ֱ�Ӹ���ճ����������С�
 4. ��������㡱��ť���������������²������������ʾ����Ҫ��������������е��ı����������������
 
##����JavaScript����˵��
��JavaScript�����а���7������������ǰ������Ϊ���㺯�������һ��Ϊ��ȡ��������������±�

| ������       | ����   |
| --------   | :-----  | 
|comp_day (day){}| ͨ���������ڼ�������ڵ�������|  
|comp_cost(day,time){}|   ͨ������ʱ�ںʹ���ʱ�䣬����ÿ������ÿСʱ�ķ���|
|comp_court (people){}| ͨ����������������Ԥ���ĳ������� |
|get_money(people){} |ͨ����������������ÿ�δ���������|
|cost_money(day,time,people){}|ͨ�����ڡ�ʱ�������������ÿ�δ�����֧��|
|earn_money(day,time,people){}|ͨ�����ڡ�ʱ�������������ÿ�δ�����ӯ��|
|in_out(){}|��ȡ��������ݣ������������|

###1��������comp_day(day){}
ͨ���������ڼ�������ڵ�������������day�ĸ�ʽΪ{yyyy-MM-dd}��ͨ������Date�����getDay()���������0��6������0��ʾ�����졢1��ʾ����һ��2��ʾ���ڶ��Դ����ơ�ͨ��console.log�ڿ���̨����������֤��������Ч�ԣ���������:
```JavaScript
function comp_day (day){    //�������ڼ�����������������Ϊ0������һΪ1�����ڶ�Ϊ2���Դ����ơ�
    var a=new Date(day); 
    return a.getDay(); 
}   
console.log(comp_day("2016-06-06"));
```
 ###2��������comp_cost(day,time){}
 ͨ�����ں�ʱ�䣬������ո�ʱÿ������ÿ��Сʱ�ķ��á�
��1����ͨ����ʱ��{1200~15:00}ͨ��.split���ա�~�����Ž��в�֣�����ֵ������timeline,����timeline�ĵ�һ��Ԫ�ر�ʾ��ʼʱ��{12:00}���ڶ���Ԫ�ر�ʾ����ʱ��{15:00}����ͨ��.split���ա�:����ʱ���ֳ��ı�{12��15}���������ı�ת��Ϊ�������ݣ��������Ի��Сʱ������s1��f1��
��2��ͨ��forѭ��Ƕ��if��䣬���㿪ʼʱ��s1�������ں�ʱ���ÿ�����صķ��ã��Կ�ʼʱ��s1�ͽ���ʱ��f1�Ĵ�С�Ƚ���Ϊѭ�������жϣ�ÿ��ѭ��ͨ��p�����ۼӼ����ÿ������ÿ�λ�ķ��á�
��3��ͨ��console.log�Է���p����������ԡ�
```JavaScript
function comp_cost(day,time){   
    var timeline = time.split("~");
    var start_time = timeline[0].split(":");
    var finish_time = timeline[1].split(":");       var s1 = parseInt(start_time[0]);
    var f1 = parseInt(finish_time[0]);  
    console.log("��ʼʱ�䣺"+s1);
    console.log("����ʱ�䣺"+f1);
    var fee = 0; var p = 0;        //fee��ʾ��λ����ÿ��Сʱ�ķ��ã�p��ʾÿ�������ڲ�ͬʱ����úϼ� 
    var days = comp_day(day);       //���ü������ڵĺ�����������ת��Ϊ������
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
console.log("����"+comp_day("2016-06-06"));
console.log("ÿ�����ػ�ѣ�"+comp_cost(comp_day ("2016-06-06"),"12:00~15:00"));  
```
###3��������comp_court(people){}��
ͨ������������������ҪԤ���ĳ���������
��1����������Ϊ���룬t��ʾ��������ȷ���ĳ�����x��ʾ��Ҫ�жϵĶ���������
��2������t��x�Ͷ������ԣ�����if�����в���ѡ���������ҪԤ���Ķ�������court��
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
 console.log("Ԥ����������"+comp_court(15));
```
###4��������get_money(people){}
ͨ����������������ÿ�δ��������롣����=����������*30��������С��4���ȡ����
```JavaScript
function get_money(people){  //����ÿ�ε����롣
    var a = 0;
    if(parseInt(people)<4){a=0;}
    else {a = parseInt(people)*30;}
    return a;
} 
```
###5��������cost_money(day,time,people){}
����ÿ�εĻ���ܷ��ã��ܷ���=ÿ�����صķ���*����������
```JavaScript
function cost_money(day,time,people) {      //����ÿ�ε��ܷ��ã�ÿ�����صķ���*����������
    var b = comp_cost(day,time)*comp_court(people);
    return b;
} 
console.log("ÿ�����طѣ�"+comp_cost("2016-06-03","09:00~12:00")+" ��������"+comp_court(14));  
```
###6��������earn_money(day,time,people){}
ͨ�����ڡ�ʱ�������������ÿ�δ�����ӯ���ʽ�ӯ��=������-��֧����
```JavaScript
function earn_money(day,time,people){         //����ӯ����ʽ�
    var e = get_money(people)-cost_money(day,time,people);
    return e;
}    
```
###7��������get_data(){}
��ȡ������е����ݣ�������һ���������顣
��1��ͨ��document.getElementById("list").value����ı�����е����ݴ������catch_text��ֻ��һ���ı������������� ����ͨ��split���ݻ��з������ݽ��в�֣���������lists��ÿ��Ԫ��ֻ��һ��ֵ��yyyy-MM-dd HH:mm~HH:mm������ͨ��forѭ����ÿ��lists��ֵ���в�֣��õ���������each_t��
```JavaScript
 function get_data(){
	var catch_text = document.getElementById("list").value;  
    var lists = catch_text.split("\n");   	 // lists��ʾ����Ĵ�����Ϣ
    console.log("���Ϣ���룺"+"\n"+catch_text);   
    console.log("�������:"+lists.length+"��");
	var each_t = new Array();   //�洢ÿ�λ�������
    for(var i=0;i<lists.length;i++){       //��ÿ����������ݴ��ڶ���each_time�У���ÿ��Ԫ�����������ԣ��ֱ������ڡ�ʱ������� ��     		
    each_t.push(lists[i].split(" "));
     }
    return each_t;
}
```
###8��deals(option){}
�Ի�ȡ�����ݽ��д�����ԭ��ֻ����������ֵ�Ķ���ת��Ϊ�����������ֵ�Ķ��󣬲����ء�����get_money(),cost_money(),earn_money(),�������롢֧����ӯ�࣬������option�����С�
```JavaScript
function deals(option){
    var days = option[0];
    var times =option[1];
    var get_s ;                           //����Ҫ�����
    var cost_s ;
    var earn_s ;	
    if (get_money(option[2])>0) {      // if�������롢֧����ӯ���������ӡ�+�����ߡ�-��
      get_s = "+"+get_money(option[2]);
      }else{
      get_s="-"+get_money(option[2]);}	        		
    cost_s="-"+cost_money(option[0],option[1],option[2]); 
    if(earn_money(option[0],option[1],option[2])>0){
        			earn_s = "+"+earn_money(option[0],option[1],option[2]);
        		} else {earn_s = earn_money(option[0],option[1],option[2]);}
        	    var t = {day:days,time:times,getMoney:get_s,costMoney:cost_s,earnMoney:earn_s};  
    return t;//���������������ʱ����tmp������        	}
```
###9��in_out()
�������������
��1����ʼͨ����ȡ������ֵ�Ƿ���ڣ����û����������ʾ��
��2�����ö�ȡ���ݵĺ���get_data()��ȡ����һ����������ݣ�����forѭ���Զ�ȡ�����ݰ���Ҫ�������ӡ�+���͡�-���Ĵ���
��3������Ҫ���ʽ�������
```JavaScript
function in_out(){           //���ݶ���ͽ�����
    if(document.getElementById("list").value.length == 0 ){ 
    alert("���������룬���������룡");
    } else{
     document.getElementById('box').innerHTML = document.getElementById('box').innerHTML+"</br>"+"[Summary]"+"</br>";           //�������
     var each_time = get_data();
     var a = each_time.length;  console.log("���Դ�����"+a);
     var sum = new Array();        //�����������飬ÿ�������д洢ÿ�εļ���������ݡ�
     var total_In = 0;
     var total_Pay = 0;
     var profit = 0;
     for(var i=0; i<a ;i++){        //���������㲢������û�����ݴ���sum�����У���ÿ��Ԫ�ذ���5�����ԣ��ֱ�Ϊ	���ڡ�ʱ�䡢���롢֧����ӯ�ࡣ
      x = each_time[i];
      var tmp = deals(x);
      sum.push(tmp);      //��tmp��������push��sum����
      total_In+=get_money(x[2]);      //�������롢֧����ӯ��
      total_Pay+=cost_money(x[0],x[1],x[2]);
      profit+=earn_money(x[0],x[1],x[2]);
      document.getElementById('box').innerHTML = document.getElementById('box').innerHTML+"</br>"+sum[i].day+" "+sum[i].time+" "+sum[i].getMoney+" "+sum[i].costMoney+" "+sum[i].earnMoney;
      }
    document.getElementById('box').innerHTML = document.getElementById('box').innerHTML+ "</br>" + "</br>"+"Total Income: "+total_In+"</br>"+"Total Payment: "+total_Pay+"</br>"+"Profit: "+profit+"</br> ";
    }
}
```
###10��������clear_text(){}��
ͨ�����ú������������������е����ݣ��Ա�����������ͼ��㡣
```JavaScript
function clear_text(){
   	console.log("�������������óɹ���");
   	document.getElementById('list').value="";
   	document.getElementById('box').innerHTML="";
}
```
 
##�ġ��ŵ��벻��
�ŵ㣺���������JavaScript���ԣ�����Chrome��������в��Ժ�չʾ����Ϊ���㡣

���㣺����չʾ������˼·����Ҫ��һЩ�ط���û����ȫ�򻯣�ʱ�����ޣ����������Ҫ�Ľ���򻯵ĵط���