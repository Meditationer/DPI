# ztree需要的js和css

- `jquery.ztree.all.min.js`树的完整js库。  
`jquery-1.4.2.js`因为基于jquery所以需要。  
css的样式：`zTreeStyle.css`,`metroStyle.css用这个`
- 参考`http://www.treejs.cn/v3/api.php`

## 树的简单配置

```html
<div>
    <ul id="treeDemo" class="ztree"></ul>
</div>
<script>
     var settingss = { }; //zTree 的参数配置
     var zNodes = [];// 数据源：zTree 的数据属性，此处使用标准json格式
     $(document).ready(function () {
         //初始化zTree，zTree容器的jquery对象/ 配置/ 节点
           zTreeObj = $.fn.zTree.init($("#treeDemo"), settingss, zNodes);
    });
</script>
```

## zTree树方法

```html
$(function(){
   loadTree();     //初始化树   没相应代码
   getTreeData();  //后台加载数据
});
$.fn.zTree:{
    init(obj,settingss,zNodes)//初始化
    getZTreeObj(treeId)
    destroy(treeId)
}
```

***

## zTree的配置(配置采用json格式)【settingss】

```html
var settingss = {//顺序可变 ---setting设置
    treeId:"",//用户定义的 zTree 容器的 id 属性值。
    treeObj:null,
    view:{},//可视界面相关配置
    edit:{},
    data:{},//数据相关配置
    check:{},//复选框相关配置
    callback:{},//各类事件的回调函数配置
    async:{ },//zTree异步加载配置
 }

```

## zTree的节点信息 【zNodes】

```json
var zNodes = [{name: "数据表",//名称
              id: 4,//id,子元素的pid
              isParent:true,//是否为父节点,默认为false
              pid:0//父节点id;data中的rootPId;
              },
              {name: "测试表",id: 1,isParent:true, pid:0},
              {name: "信息表",id: 2,isParent:true, pid:0},
              {name: "作废表",id: 3,isParent:true, pid:0}
            ];
```

### async:{ },异步加载配置

```js
//必须操作
enable: true,//是否开启异步加载模式
url:"./zTreeDemoV9.0SimpleFromV10.0.php",//请求地址
// 举例：添加属性
autoParam: ["id=parentId","name"]//对父节点 node = {id:1, name:"test"}进行异步，将提交parentId和name.
contentType: "application/json",//设置提交时候为json格式
//ajax请求后的数据预处理函数
dataFilter: function(treeId,parentNode,responseData){
      for(var i=0;i<responseData.length;i++){
        responseData[i] = JSON.parse(responseData[i])
      }
      return responseData;
    }
```

### callback:回调函数配置

```js
//回调错误事件  onAsyncError:方法名
 onAsyncError: function(event, treeId, treeNode, XMLHttpRequest, textStatus, errorThrown){
      alert("初始化节点数据失败,请稍后重试");
    },
    //回调成功事件
    onAsyncSuccess: function(event, treeId, treeNode, resData){
      var zTree = $.fn.zTree.getZTreeObj("treeDemo");
      console.log("数据加载成功");
      var count = (treeNode.children.length);
      //加载成功后;在节点后面显示此父节点下有几个一级子节点
      $(".ztree").find("a[title="+treeNode.name+"]").find("span[class='node_name']").html(treeNode.name+"<span>("+count+")</span>");
    },
    //父节点展开时的事件
    onExpand: function(event, treeId, treeNode){
      //zTree对象
      var zTree = $.fn.zTree.getZTreeObj("treeDemo");
      //获取点击的id
      var nowId = treeNode.id;
      //获取所有节点
      var allNodes = zTree.getNodes();
      //获取点击节点的层级
      var level = treeNode.level;
      //定义过滤函数;获取节点层级与点击节点层级相同并且为父节点的节点
      function filter(node) {
        return (node.level == treeNode.level && node.isParent);
      }
      //获得点击节点同级的父节点的集合
      var sameLevelNodes = zTree.getNodesByFilter(filter);
      //遍历同级节点集合
      for(var i=0;i<sameLevelNodes.length;i++){
        //将非被点击父节点收起;实现手风琴效果
        if(sameLevelNodes[i].id != nowId){
          zTree.expandNode(sameLevelNodes[i], false, true, true);
        }
      }
    },
    //点击事件
    onClick: function(e, treeId, treeNode, clickFlag) {
      //tree实例
      var zTree = $.fn.zTree.getZTreeObj("treeDemo");
      //点击文字关联复选框
      //如果不是父节点,则关联,或者是父节点,但展开状态位true是,也关联;
      if(!treeNode.isParent || (treeNode.isParent && treeNode.open)){
        zTree.checkNode(treeNode, !treeNode.checked, true);//点击文字关联复选框
      }
      //点击文字展开当前节点
      zTree.expandNode(treeNode, true, true, true);
      // zTree.reAsyncChildNodes(treeNode, "refresh");//强行异步加载(存在子节点也进行加载)
      //手风琴效果;直接调用onExpand
      zTree.setting.callback.onExpand(e, treeId, treeNode);
      //点击节点名称和勾选节点前面的复选框逻辑相同;
      //直接在onClick里面调用onCheck函数;并传入所需参数
      zTree.setting.callback.onCheck(e, treeId, treeNode);
    },
```

### 关于data

```js
simpleData:{enable:true},//使用简单数据模式
```
