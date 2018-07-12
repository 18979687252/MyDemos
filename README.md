```
/**
 * 判断是否为空
 * @param    m
 * @return {Boolean}
 */
function isExist(m){
	if(m == '' || m == null || typeof(m) == undefined ){
		return false
	}else if(Object.prototype.toString.call(m)=='[object Array]'){
		if(m.length == 0){
			return false
		}else {
			return true
		}
	}else if ( typeof(m) == 'object'){
		for(var key in m){
			if(!m[key]){
				return false
			}else {
				return true
			}
		}
	}
}
/**
 * 判断是否为月末
 * @param  date
 * @return boolean
 */
function monthLastDay (date) {
  let monthArr_b = [1,3,5,7,8,10,12]
  let monthArr_s = [2,4,6,8,9,11]
  let myDate = new Date(date)
  let year = myDate.getFullYear()
  let month = myDate.getMonth() + 1
  let dd = myDate.getDate()
  let isLeap = isLeapYear(year)
  let index_b = monthArr_b.findIndex((x) =>{
    return x == month
  })
  let index_s = monthArr_s.findIndex((x) =>{
    return x == month
  })
  if(index_b > -1){
    if(dd == 31){
      return true
    }else{
      return false
    }
  }else if(index_s > -1){
    if(month == 2) {
      if (isLeap && dd == 29 || !isLeap && dd == 28) {
        return true
      }else{
        return false
      }
    }else{
      if(dd == 30){
        return true
      }else{
        return false
      }
    }
  }
}
/**
 * 判断是否为闰年
 * @param  year
 * @return {Boolean}
 */
function isLeapYear(year) {
  return (year % 4 == 0) && (year % 100 != 0 || year % 400 == 0);
}

/**
 * 判断是否为周五
 * @param  date
 * @return {Boolean}
 */
function isFriday (date) {
  let myDate = new Date(date)
  let day = myDate.getDay()
  if(day == 5){
    return true
  }else{
    return false
  }
}

/**
 * 创建并下载文件
 * @param  {String} fileName 文件名
 * @param  {String} content  文件内容
 */
function createAndDownloadFile(fileName, content) {
    var aTag = document.createElement('a');
    var blob = new Blob([content]);
    aTag.download = fileName;
    aTag.href = URL.createObjectURL(blob);
    aTag.click();
    URL.revokeObjectURL(blob);
}

/*
* 获取某年某月第一天和最后一天
*/
function getFirstAndLastMonthDay( year, month){
     var firstdate = year + '-' + month + '-01';
     var day = new Date(year,month,0);
     var lastdate = year + '-' + month + '-' + day.getDate();//获取当月最后一天日期
     return {firstdate,lastdate}
}

/*
* url拼接参数
*/
function encodeSearchParams(url,params) {
    const paramsArr = []
    Object.keys(params).forEach((key) => {
        let value = params[key]
        // 如果值为undefined我们将其置空
        if (typeof value === 'undefined') {
            value = ''
        }
        // 对于需要编码的文本（比如说中文）我们要进行编码
        paramsArr.push([key, encodeURIComponent(value)].join('='))
    })
    return `${url}?${paramsArr.join('&')}`
}
//网上比较经典的js获取url中的参数的方法
 //但是在使用的过程中，发现其在获取中文参数的时候，获取到的值是乱码的
 //解决办法:将解码方式unscape换为decodeURI
 //原因:浏览器会将url中的中文参数进行encodeURI编码，所以要通过js使用decodeURI进行解码
function getQueryString(name) {
    var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)", "i");
    var r = window.location.search.substr(1).match(reg);
    if ( r != null ){
       return unescape(r[2]);
    }else{
       return null;
    }
 }

```