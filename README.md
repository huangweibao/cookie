# cookie
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">  
<html xmlns="http://www.w3.org/1999/xhtml">  
<head>  
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />  
<title>无标题文档</title>  
<script language="javascript" type="text/javascript">  
function addCookie(name,value,days,path){   /**添加设置cookie**/  
    var name = escape(name);  
    var value = escape(value);  
    var expires = new Date();  
    expires.setTime(expires.getTime() + days * 3600000 * 24);  
    //path=/，表示cookie能在整个网站下使用，path=/temp，表示cookie只能在temp目录下使用  
    path = path == "" ? "" : ";path=" + path;  
    //GMT(Greenwich Mean Time)是格林尼治平时，现在的标准时间，协调世界时是UTC  
    //参数days只能是数字型  
    var _expires = (typeof days) == "string" ? "" : ";expires=" + expires.toUTCString();  
    document.cookie = name + "=" + value + _expires + path;  
}  
function getCookieValue(name){  /**获取cookie的值，根据cookie的键获取值**/  
    //用处理字符串的方式查找到key对应value  
    var name = escape(name);  
    //读cookie属性，这将返回文档的所有cookie  
    var allcookies = document.cookie;         
    //查找名为name的cookie的开始位置  
    name += "=";  
    var pos = allcookies.indexOf(name);      
    //如果找到了具有该名字的cookie，那么提取并使用它的值  
    if (pos != -1){                                             //如果pos值为-1则说明搜索"version="失败  
        var start = pos + name.length;                  //cookie值开始的位置  
        var end = allcookies.indexOf(";",start);        //从cookie值开始的位置起搜索第一个";"的位置,即cookie值结尾的位置  
        if (end == -1) end = allcookies.length;        //如果end值为-1说明cookie列表里只有一个cookie  
        var value = allcookies.substring(start,end); //提取cookie的值  
        return (value);                           //对它解码        
    }else{  //搜索失败，返回空字符串  
        return "";  
    }  
}  
function deleteCookie(name,path){   /**根据cookie的键，删除cookie，其实就是设置其失效**/  
    var name = escape(name);  
    var expires = new Date(0);  
    path = path == "" ? "" : ";path=" + path;  
    document.cookie = name + "="+ ";expires=" + expires.toUTCString() + path;  
}  
  
/**实现功能，保存用户的登录信息到cookie中。当登录页面被打开时，就查询cookie**/  
window.onload = function(){  
    var userNameValue = getCookieValue("userName");  
    document.getElementById("txtUserName").value = userNameValue;  
    var userPassValue = getCookieValue("userPass");  
    document.getElementById("txtUserPass").value = userPassValue;  
}  
  
function userLogin(){   /**用户登录，其中需要判断是否选择记住密码**/  
    //简单验证一下  
    var userName = document.getElementById("txtUserName").value;  
    if(userName == ''){  
        alert("请输入用户名。");  
        return;  
    }  
    var userPass = document.getElementById("txtUserPass").value;  
    if(userPass == ''){  
        alert("请输入密码。");  
        return;  
    }  
    var objChk = document.getElementById("chkRememberPass");  
    if(objChk.checked){  
        //添加cookie  
        addCookie("userName",userName,7,"/");  
        addCookie("userPass",userPass,7,"/");  
        alert("记住了你的密码登录。");  
        window.location.href = "http://www.baidu.com";  
    }else{  
        alert("不记密码登录。");  
        window.location.href = "http://www.baidu.com";  
    }  
}  
</script>  
</head>  
<body>  
<center>  
    <table width="400px" height="180px" cellpadding="0" cellspacing="0" border="1" style="margin-top:100px;">  
        <tr>  
            <td align="center" colspan="2">欢迎使用XXX管理系统</td>  
        </tr>  
        <tr>  
            <td align="right">  
                <label>用户名：</label>  
            </td>  
            <td align="left">  
                <input type="text" id="txtUserName" name="txtUserName" style="width:160px; margin-left:10px;" />  
            </td>  
        </tr>  
        <tr>  
            <td align="right">  
                <label>密  码：</label>  
            </td>  
            <td align="left">  
                <input type="password" id="txtUserPass" name="txtUserPass" style="width:160px; margin-left:10px;" />  
            </td>  
        </tr>  
        <tr>  
            <td align="center" colspan="2">  
                <span style="font-size:12px; color:blue; vertical-align:middle;">是否记住密码</span>  
                <input type="checkbox" id="chkRememberPass" name="chkRememberPass" style="vertical-align:middle;" />  
            </td>  
        </tr>  
        <tr>  
            <td align="center" colspan="2">  
                <input type="submit" id="subLogin" name="subLogin" value="登 录" onclick="userLogin()"/>  
                      
                <input type="reset" id="resetLogin" name="resetLogin" value="重 置" />  
            </td>  
        </tr>  
    </table>  
</center>  
</body>  
</html>  
