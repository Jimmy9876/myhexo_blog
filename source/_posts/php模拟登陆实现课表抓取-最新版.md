---
title: php模拟登陆实现课表抓取(最新版)
copyright: true
date: 2017-05-26 15:13:01
tags: php
---

> 首先，简单的说下表单原理，当我们在正方输入学号、密码、验证码的时候，点击提交按钮会产生一个POST请求，服务器在接受到POST请求以后，检查提交的学号密码验证码是否正确，正确则登陆成功。

环境：Mac+MAMP Pro+phpstorm(PHP7.1)+Chrome

## 1、抓包

打开谷歌浏览器访问学校教务处网址，打开开发者工具选择network，之后在正方里填上你的学号，密码，验证码，登录，看看这期间提交的数据。

![](http://i1.piimg.com/588926/fa6f6f661397058c.jpg)

我们要用到的数据只有default2.aspx和xs_main.aspx?xh=”你的学号”这两个，其余的都是修饰用的css文件。点开default2.aspx可以看到你提交的表单数据。

![](http://i1.piimg.com/588926/e2468014006c83be.jpg)

其中__VIEWSTATE是asp.net服务器的状态信息，需要抓取出来。
另外default2.aspx这个页面采用了302跳转，即登录成功后会跳转到xs_main.aspx?xh=”你的学号”这个网址，这一点可能是大多数人模拟登录失败的原因。

## 2、构造登录页面

三项信息必填，学号、密码、验证码。先说说验证码怎么保存到本地。

![](http://i4.buimg.com/588926/7d45a6e1eff2d946.jpg)

验证码是由一个叫checkcode.aspx的网页生成的，要保存可以用`fwrite`来实现。直接用`<img src=""`填上刚才的网址理论上也可以，只要你能保存下这张图片所对应的cookie，这个cookie决定了你是否能够进行后续数据抓取。

具体代码如下：

首先要新建一个cookie文件夹，并且把session打开（可以解决高并发访问时登陆失败的问题）。

```php
<?php 
    session_start();
    $id=session_id();
    $_SESSION['id']=$id;
?>
```

验证码保存：

这里注意⚠️要自己新建一个`cookie`文件夹📁在你的项目目录。

```php
<?php 
  	$cookie = dirname(__FILE__) . '/cookie/'.$_SESSION['id'].'.txt'; //cookie路径
	$verify_code_url = "http://你的正方网址/CheckCode.aspx"; //验证码地址
	$curl = curl_init();
	curl_setopt($curl, CURLOPT_URL, $verify_code_url);
	curl_setopt($curl, CURLOPT_COOKIEJAR, $cookie);  //保存cookie
	curl_setopt($curl, CURLOPT_HEADER, 0);
	curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
	$img = curl_exec($curl);  //执行curl
	curl_close($curl);
	$fp = fopen("verifyCode.jpg","w");  //文件名
	fwrite($fp,$img);  //写入文件
	fclose($fp);
?>
```

之后构造`input`表单，设置好`name`

```Html
<form name="form1" method="post" action="kebiao.php" >
    用户名:<input type="text" name="xh" /><!--普通文本框-->
    密码:<input type="password" name="pw" /><!--密码框-->
    验证码:<input type="text" name="code" /><img src="verifyCode.jpg">
    <input type="submit" value="提交信息" />
</form>
```

## 3、后端模拟登录页面

```php
<?php
/**
 * Created by PhpStorm.
 * User: Apple
 * Date: 2019/5/17
 * Time: PM9:08
 */
session_start();
header("Content-type: text/html; charset=gb2312");  //视学校而定，博主学校是gbk编码，php也采用的gbk编码方式

//将表格转换成数组函数
function get_td_array($table) {
    $table = preg_replace("'<table[^>]*?>'si","",$table);
    $table = preg_replace("'<tr[^>]*?>'si","",$table);
    $table = preg_replace("'<td[^>]*?>'si","",$table);
    $table = str_replace("</tr>","{tr}",$table);
    $table = str_replace("</td>","{td}",$table);
    //去掉 HTML 标记
    $table = preg_replace("'<[/!]*?[^<>]*?>'si","",$table);
    //去掉空白字符
    $table = preg_replace("'([rn])[s]+'","",$table);
    $table = preg_replace('/&nbsp;/',"",$table);
    $table = str_replace(" ","",$table);
    $table = str_replace(" ","",$table);
    $table = explode('{tr}', $table);
    array_pop($table);
    foreach ($table as $key=>$tr) {
        $td = explode('{td}', $tr);
        array_pop($td);
        $td_array[] = $td;
    }
    return $td_array;
}

function login_post($url, $cookie, $post)
{
    $ch = curl_init();
    curl_setopt($ch, CURLOPT_URL, $url);
    curl_setopt($ch, CURLOPT_HEADER, 0);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);  //不自动输出数据，要echo才行
    curl_setopt($ch, CURLOPT_FOLLOWLOCATION, 1);  //重要，抓取跳转后数据
    curl_setopt($ch, CURLOPT_COOKIEFILE, $cookie);
    curl_setopt($ch, CURLOPT_REFERER, 'http://202.119.225.34/');  //重要，302跳转需要referer，可以在Request Headers找到
    curl_setopt($ch, CURLOPT_POSTFIELDS, $post);  //post提交数据
    $result = curl_exec($ch);
//    $content = curl_getinfo($ch);
//    echo json_encode($content);
    curl_close($ch);
    return $result;
}

$_SESSION['xh'] = $_POST['xh'];
$xh = $_POST['xh'];
$pw = $_POST['pw'];
$code = $_POST['code'];
$cookie = dirname(__FILE__) . '/cookie/' . $_SESSION['id'] . '.txt';
$url = "http://202.119.225.34/default2.aspx";
$con1=login_post($url,$cookie,'');
    preg_match_all('/<input type="hidden" name="__VIEWSTATE" value="([^<>]+)" \/>/', $con1, $view); //获取__VIEWSTATE字段并存到$view数组中
    $post=array(
        '__VIEWSTATE'=>$view[1][0],
        'txtUserName'=>$xh,
        'TextBox2'=>$pw,
        'txtSecretCode'=>$code,
        'RadioButtonList1'=>'%D1%A7%C9%FA',  //“学生”的gbk编码
        'Button1'=>'',
        'lbLanguage'=>'',
        'hidPdrs'=>'',
        'hidsc'=>''
    );
    $con2=login_post($url,$cookie,http_build_query($post)); //将数组连接成字符串
    preg_match_all('/<span id="xhxm">([^<>]+)/', $con2, $xm);
	$xm[1][0] = substr($xm[1][0], 0, -4);
$url2 = "http://202.119.225.34/xskbcx.aspx?xh=" . $_SESSION['xh'] . "&xm=" . $xm[1][0];
$con3 = login_post($url2, $cookie, '');

//echo $con3;
print_r($con3);
?>
```

如果代码都正确，你将看到如下页面

![](http://i4.buimg.com/588926/eda145ce10fe2f0a.png)



![](http://i4.buimg.com/588926/fad605f358e06ff5.png)

课表成功拿到。

同理可以用正则表达式拿到成绩等，可以用这些数据做个微信公众号用来查询成绩课表等等。这些以后有时间再深入了解。

