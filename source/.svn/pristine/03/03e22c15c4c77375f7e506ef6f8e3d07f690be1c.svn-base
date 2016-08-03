---
title: 下拉菜单插件(内部开发)代码和使用说明
date: 2016-05-05 09:09:35
categories: [categories1,categories2]

tags: 

- 插件

---

<link href="http://cdn.bootcss.com/highlight.js/8.0/styles/monokai_sublime.min.css" rel="stylesheet">  
<script src="http://cdn.bootcss.com/highlight.js/8.0/highlight.min.js"></script>  
<script>
	hljs.initHighlightingOnLoad();
</script>  

> 本插件代码路径:[src\module\common\select-box\select.js & select.html](http://192.168.60.251/svn/xian-new/pva_project/trunk/src/module/common/select-box)
> @author songxj
> @date 2015-10-16

## 代码

	define(["ajaxModel", "jquery", 'handlebars'], function(ajaxModel, jQuery) {
    	return (function (scope, $) {
	        var
	            _templateHtml = null, // 缓存模板列表
	            _templateURL = "/module/common/select-box/select.html", // 模版请求地址
	            
### _calculatePubdivPosition 计算下拉列表宽度和位置

> 计算下拉列表的宽度和位置,并给下拉列表容器元素添加相对应css属性
> @param  {[type]} $selector [文本框元素]
> @param  {[type]} $pubdiv   [下拉列表容器元素]

	            _calculatePubdivPosition = function ($selector, $pubdiv) {
	                var selectorWidth = $selector.width(),
	                    selectorHeight = $selector.height(),
	                    offset = $selector.offset(),
	                    selectorLeft = offset.left,
	                    selectorTop = offset.top;
	                $pubdiv.width(selectorWidth).css("left", selectorLeft).css("top", (selectorTop + selectorHeight)).show();
	            },

### _dealCheckboxChooseStyle 处理下拉列表中checkbox选中样式

> @param  {[type]} $this [下拉列表中checkbox行元素]

	            _dealCheckboxChooseStyle = function($this) {
	                var $currentCheckbox = $this.find("i.checkbox"),
	                    $allCheckboxs = $this.closest(".pubdiv").find("i.checkbox"),
	                    isSelectedAllFlag = true,
	                    liType = $this.attr("data-value");
	
	                // 实现checkbox全选、选中、取消选中
	                if (liType === "-1") { // 全选
	                    $currentCheckbox.hasClass("active") ? $allCheckboxs.removeClass("active") : $allCheckboxs.addClass("active");
	                } else { // 非全选
	                    if ($currentCheckbox.hasClass("active")) { // 取消选中
	                        $currentCheckbox.removeClass("active");
	                        // 让全选不选中
	                        $allCheckboxs.first().removeClass("active");
	                    } else { // 选中
	                        $currentCheckbox.addClass("active");
	                        // 让全选选中
	                        $allCheckboxs.each(function() {
	                            if (!$this.hasClass("active") && $this.closest("li").attr("data-value") !== "-1") {
	                                isSelectedAllFlag = false;
	                                return false;
	                            }
	                        });
	                        if (isSelectedAllFlag) { // 让全选checkbox选中
	                            $allCheckboxs.first().addClass("active");
	                        }
	                    }
	                }
	            },

### _dealSelectListMuliSelect 处理下拉列表多选情况

> @param  {[type]}   $this     [下拉列表中checkbox行元素]
> @param  {[type]}   $selector [文本框元素]
> @param  {Function} callback  [回调函数]
 
	            _dealSelectListMuliSelect = function($this, $selector, callback) {
	                var $allCheckboxs = $this.closest(".pubdiv").find("i.checkbox"),
	                    selectorClass = $selector.attr("class"),
	                    mutiliCallbackData = {selector: selectorClass, data:[]};
	
	                // 处理checkbox选中样式
	                _dealCheckboxChooseStyle($this);
	
	                // 拼凑callback返回的数据
	                $allCheckboxs.each(function() {
	                    if ($(this).hasClass("active") && $(this).closest("li").attr("data-value") !== "-1") {
	                        mutiliCallbackData.data.push({name: $(this).siblings("em").text(), value: $(this).closest("li").attr("data-value")});
	                    }
	                });
	
	                // 执行回调函数
	                callback && callback(mutiliCallbackData);
	            },
 
### _dealNormalSelectList 处理正常的下拉列表的情况

> @param  {[type]}   $this     [下拉列表行元素]
> @param  {[type]}   $selector [文本框元素]
> @param  {Function} callback  [回调函数]

	            _dealNormalSelectList = function($this, $selector, callback) {
	                var $selectorField = $selector.find(".text"),
	                    selectorClass = $selector.attr("class"),
	                    liType = $this.attr("data-value"),
	                    callbackData = {selector: selectorClass, data:{}},
	                    text = $this.text();
	
	                // 将值写入下拉框,并删除下拉列表
	                $selectorField.attr("data-value", liType).text(text);
	                _switchArrow($this.closest(".pubdiv").siblings(".select_container"));
	                $this.closest(".pubdiv").remove();
	
	                // 给callback返回的数据写值
	                callbackData.data["name"] = text;
	                callbackData.data["value"] = liType;
	
	                // 执行回调函数
	                callback && callback(callbackData);
	            },

### _bindSelectListEvent 下拉列表事件

> @author songxj
> @param  {[type]}   $selector   [文本框元素]
> @param  {[type]}   selectModle [下拉列表类型 multiSelect：多选  其他：非多选]
> @param  {Function} callback    [回调函数]

	            _bindSelectListEvent = function ($selector, selectModle, callback) {
	                /*下拉列表中下拉项的点击事件*/
	                $(".select_wrapper .pubdiv li").on("click", function() {
	                    if (selectModle === "multiSelect") { // 多选，肯定有回调函数
	                        // 处理下拉列表多选情况
	                        _dealSelectListMuliSelect($(this), $selector, callback);
	                    } else { // 非多选，有回调函数时执行回调函数
	                        // 处理正常的下拉列表的情况
	                        _dealNormalSelectList($(this), $selector, callback);
	                    }
	                });
	
	                /*下拉列表hover事件：标记当前鼠标是否离开下拉列表的状态*/
	                $(".select_wrapper .pubdiv").hover(function() {
	                    $(this).removeClass("leave");
	                }, function() {
	                    $(this).addClass("leave");
	                });
	            },

### _switchArrow 切换向上、向下箭头

> @param  {[type]} $selector [文本框元素]

	            _switchArrow = function ($selector) {
	                var $pubdiv = $selector.siblings(".pubdiv"),
	                    $arrow = $selector.find(".arrow");
	
	                $pubdiv.is(":visible") ? $arrow.addClass("arrow-down").removeClass("arrow-up") : $arrow.addClass("arrow-up").removeClass("arrow-down");
	            },

### _drawTemplateCallback 渲染模板的回调函数

> @param  {[type]} $selector [文本框元素]
> @param  {[type]} params    [参数列表]

	            _drawTemplateCallback = function ($selector, params) {
	                var $selectWrapper = $selector.closest(".select_wrapper"),
	                    tempData = {};
	
	                tempData[params.selectModle] = {"data": params.data};
	                $selectWrapper.append(_templateHtml(tempData));
	
	                // 给下拉列表做个标记：当前的下拉框
	                $selectWrapper.find(".pubdiv").attr("data-selector", params.selector);
	
	                // 计算下拉列表的宽度和位置
	                _calculatePubdivPosition($selector, $selectWrapper.find(".pubdiv"));
	
	                // 绑定下拉列表事件
	                _bindSelectListEvent($selector, params.selectModle, params.callback);
	            },

### _getSelectorData 获取下拉列表数据

> @param  {[type]} $selector [文本框元素]
> @param  {[type]} params    [参数列表]

	            _getSelectorData = function ($selector, params) {
	                var selectModle = null;
	
	                // 判断当前下拉框的模板类型
	                if (!params.isMultiSelect) { // 不是多选下拉列表
	                    selectModle = "normal";
	                } else { // 多选下拉列表
	                    selectModle = "multiSelect";
	                }
	                params["selectModle"] = selectModle;
	
	                // 若模板不存在则重新发送请求加载，若存在则根据模板加载数据并显示
	                if (_templateHtml) {
	                    _drawTemplateCallback($selector, params);
	                } else {
	                    ajaxModel.getTml(_templateURL).then(function(result) {
	                        _templateHtml = Handlebars.compile(result); //缓存模板
	                        _drawTemplateCallback($selector, params);
	                    });
	                }
	            },

### _bindEvents 下拉文本框元素、document事件

> @param  {[type]} params [参数列表]

	            _bindEvents = function (params) {
	                /*下拉文本框元素点击事件：显示加载下拉列表*/
	                $(params.selector).on("click", function(e) {
	                    var $this = $(this),
	                        $selectWrapper = $this.closest(".select_wrapper"),
	                        $panel = $(".select_wrapper .pubdiv");
	
	                    // 阻止事件冒泡
	                    e.stopPropagation();
	
	                    // 若界面上有下拉列表，则删除
	                    if ($panel.length) {
	                        _switchArrow($(".select_wrapper .pubdiv").closest(".select_wrapper").find(".select_container"));
	                        $(".select_wrapper .pubdiv").remove();
	
	                        // 若点击的是当前下拉框,return
	                        if ($panel.attr("data-selector") === params.selector) {
	                            return;
	                        }
	                    }
	
	                    // 切换当前下拉元素的箭头
	                    _switchArrow($this);
	
	                    // 获取对应下拉列表数据
	                    _getSelectorData($this, params);
	                });
	
	                /*document点击事件：点击非下拉列表时，将当前下拉列表删除*/
	                if (!this.inited) {
	                    $(document).on("click", function(e) {
	                        if ($(".select_wrapper .pubdiv").hasClass("leave")) {
	                            _switchArrow($(".select_wrapper .pubdiv").closest(".select_wrapper").find(".select_container"));
	                            $(".select_wrapper .pubdiv").remove();
	                        }
	                    });
	                    this.inited = true;
	                }
	            };

### selectBox 下拉列表入口]

> @param  {[type]} options [参数列表]

	        scope.selectBox = function (options) {
	           if (options instanceof Array) { // 数组：多个下拉框
	                for (var i = 0, optionLength = options.length; i < optionLength; i++) {
	                    _bindEvents(options[i]);
	                }
	           } else { // 对象：一个下拉框
	                _bindEvents(options);
	           }
	        };
> return scope
	
	        return scope;
	    }({}, jQuery));
	});
