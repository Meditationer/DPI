# ztree需要的js和css

- `jquery.ztree.all.min.js`树的完整js库。  
`jquery-1.4.2.js`因为基于jquery所以需要。  
css的样式：`zTreeStyle.css`,`metroStyle.css用这个`

## 树的简单配置

```html
<div>
    <ul id="treeDemo" class="ztree"></ul>
</div>
<script>
     var settingss = { }; //zTree 的参数配置
     var zNodes = [];// 数据源：zTree 的数据属性，此处使用标准json格式
     $(document).ready(function () {
         //初始化zTree，三个参数分别是容器(zTree的容器就是id 别忘了设置为 "ztree")、参数配置、数据源
           zTreeObj = $.fn.zTree.init($("#treeDemo"), setting, zNodes);
    });
</script>
```

## zTree的配置(配置采用json格式)

- 配置分为view（可视界面相关配置）、data（数据相关配置）、check（复选框相关配置）、callback（各类事件的回调函数配置）、async（zTree异步加载配置）

```html
var settingss = {//顺序可变
    view:{//不写会给默认值
        showIcon: true,  //设置是否显示节点图标
        showTitle: true,  //设置是否显示节点的title提示信息
        },
    data:{
        key: {title: "title"}, // 节点数据保存属性名称
        },
    async:{},
 }

```
