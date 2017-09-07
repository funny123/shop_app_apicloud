//判断是否ios
function isIOS() {
	return api.systemType == "ios";
}

/************ 判断是否登录. ****************/
function doLogin(name) {
	var user = $api.getStorage('user');
	if (user) {
		return;
	} else {
		api.alert({
			title : '提示',
			msg : '请先登录',
			buttons : ['确定']
		}, function(ret, err) {
			if (ret) {
				return;
			}
		});

	}
}

function goLogin() {
	var user = $api.getStorage('user');
	if (user) {
		return;
	} else {
		if (api.systemType == "ios") {
			var times = 0;
		} else {
			var times = 300;
		}
		api.openWin({
			name : 'login',
			url : '../login/login_head.html',
			delay : times
		});
	}
}

function openWinto(name, url, str) {//打开新窗口//str参数
	if (api.systemType == "ios") {
		var times = 0;
	} else {
		var times = 300;
	}
	api.openWin({
		name : name,
		url : url + '.html',
		delay : times,
		slidBackType : 'edge',
		pageParam : {
			param : str

		}
	});
}

function openWin(name, url, islogin, no) {//打开新窗口并且需要验证登录
	if (api.systemType == "ios") {
		var times = 0;
	} else {
		var times = 300;
	}
	if (islogin) {//判断是否需要登录验证
		var user = $api.getStorage('user');
		if (!user) {
			api.alert({
				title : '提示',
				msg : '请先登录',
				buttons : ['确定']
			});
			return;
		} else {
			api.openWin({
				name : name,
				url : url + '.html',
				delay : times,
				slidBackType : 'edge'
			});
		}
	}
}

function toast(text, location) {
	api.toast({
		msg : text,
		location : location
	});
}

function openFrame(name, url) {//打开一个子窗口,一般用于打开分享页面
	api.openFrame({
		name : name,
		url : url + '.html',
		rect : {
			x : 0,
			y : 80,
		},
		bounces : false
	});
}

function call(tel) {
	api.call({
		type : 'tel_prompt',
		number : tel
	});
}

/*搜索相关方法*/
function doSearch() {
	$api.addCls($api.dom(".aui-searchbar-wrap"), "focus");
	$api.dom('.aui-searchbar-input input').focus();
}

function cancelSearch() {
	$api.removeCls($api.dom(".aui-searchbar-wrap.focus"), "focus");
	$api.val($api.byId("search-input"), '');
	$api.dom('.aui-searchbar-input input').blur();
}

function clearInput() {
	$api.val($api.byId("search-input"), '');
}

function search() {
	var content = $api.val($api.byId("search-input"));
	if (content) {
		$api.setStorage('keyword', content);
		api.setFrameGroupIndex({
			name : 'main',
			index : 3
		});
		var jsfun = 'window.location.reload();';
		api.execScript({
			name : 'root',
			frameName : 'footer_tab_4',
			script : jsfun
		});
		//		api.alert({
		//			title : '搜索提示',
		//			msg : '您输入的内容为：' + content
		//		});
	} else {
		api.alert({
			title : '搜索提示',
			msg : '您没有输入任何内容'
		});
	}
	cancelSearch();
}

/*扫一扫 二维码扫描*/
function doScanner() {
	var FNScanner = api.require('FNScanner');
	FNScanner.openScanner({
		sound : 'widget://res/bi.wav',
		autorotation : true,
	}, function(ret, err) {
		if (ret) {
			if (ret.eventType == 'success') {
				alert(JSON.stringify(ret.content));
			}
		} else {
			alert(JSON.stringify(err));
		}
	});
}

//商品详情
function openGoods(url, no, name, price, images) {//打开新窗口并且需要验证登录
	if (api.systemType == "ios") {
		var times = 0;
	} else {
		var times = 300;
	}

	api.openWin({
		name : 'goods_content',
		url : url + '.html',
		delay : times,
		slidBackType : 'edge',
		pageParam : {
			goods_no : no,
			goods_name : name,
			goods_price : price,
			goods_images : images
		}
	});

}

//商品详情-搜索
function openGoods2(url, no) {//打开新窗口并且需要验证登录
	if (api.systemType == "ios") {
		var times = 0;
	} else {
		var times = 300;
	}

	api.openWin({
		name : 'goods_content',
		url : url + '.html',
		delay : times,
		slidBackType : 'edge',
		pageParam : {
			goods_no : no
		}
	});

}

//订单详情
function openOrder(url, ordername) {//打开新窗口并且需要验证登录
	if (api.systemType == "ios") {
		var times = 0;
	} else {
		var times = 300;
	}

	api.openWin({
		name : 'order_detail_head',
		url : url + '.html',
		delay : times,
		slidBackType : 'edge',
		pageParam : {
			ordername : ordername
		}
	});

}

//打开商品列表
function openWinToType(clsno) {//打开新窗口
	if (api.systemType == "ios") {
		var times = 0;
	} else {
		var times = 300;
	}
	api.openFrame({
		name : 'sort2',
		url : './sort2.html',
		rect : {
			x : 0,
			y : $api.getStorage('headerh'),
			w : 'auto',
			h : $api.getStorage('bodyh') - $api.getStorage('headerh') - $api.getStorage('footerh')
		},
		bounces : false,
		pageParam : {
			clsno : clsno
		}
	});
	//	api.openWin({
	//		name : 'sort2',
	//		url : './sort2.html',
	//		delay : times,
	//		slidBackType : 'edge',
	//		pageParam : {
	//			clsno : clsno
	//		}
	//	});
}

// 获取信息
function headList(page) {

	api.showProgress({
		title : '加载中',
		modal : false
	});
	api.ajax({
		url : 'http://www.ghuog.com/yii2_shop/api/web/app/v1?job=test&skey=' + $api.getStorage('keyword') + '&page=' + page + '&loginname=' + $api.getStorage('loginname') + '',
		method : 'get',
		data : {
			values : {
			}
		}
	}, function(ret, err) {
		if (ret) {
			//					alert(JSON.stringify(ret));
			//			$api.html($api.byId('goods_list'), '');
			if (ret.data.length <= 0) {
				api.toast({
					msg : '没有了',
					location : 'bottom'
				});
				api.hideProgress();
				api.refreshHeaderLoadDone();
			}
			//					var app = new Vue({
			//						el : "#goods_list",
			//						data : {
			//							result : ret.data
			//						}
			//					})
			for (var i = 0; i <= ret.data.length - 1; i++) {
				var html = '<li class="aui-list-view-cell aui-img aui-counter-list" tapmode onclick="openGoods2(\'../html/goods/goods_content\',\'' + ret.data[i].no + '\')">';
				html = html + '<img class="aui-img-object aui-pull-left" src="' + ret.data[i].images + '" data-echo="' + ret.data[i].images + '">';
				html = html + '<div class="aui-img-body">';
				html = html + '<div class="aui-text-default aui-ellipsis-1">' + ret.data[i].name + '</div>';
				html = html + '<span class="aui-carfont aui-ellipsis-1">' + ret.data[i].no + '</span>';
				html = html + '<div class="aui-counter-box">';
				html = html + '<div class="aui-pull-left aui-text-danger">' + ret.data[i].price + '</div>';
				html = html + '<div class="aui-text-default aui-pull-right"></div>';
				html = html + '</div>';
				html = html + '</div>';
				html = html + '</li>';
				$api.prepend($api.byId('goods_list'), html);
				api.hideProgress();
				api.refreshHeaderLoadDone();
				//						//					dataLoading = false;
				//						//					fnCacheImage(ret, 0);
			}
		} else {
			api.alert({
				msg : JSON.stringify(err)
			});
		}
	});
}

