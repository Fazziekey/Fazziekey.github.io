---
title: 建立你的知识神经网络
toc: true
copyright: true
date: 2020-08-08 15:20:11
tags:
    - JavaScript
    - hexo
categories:
    - 《栈溢出工程师》
reward:
---
早在6月份学习深度学习的时候就有想在自己的博客中加入一张神经网络图记录学习的知识体系，一直拖到现在（主要是看门狗2太好玩了，不是）。这篇文章将详细的介绍如何在hexo博客中加入一张神经网络图。

<!--more-->

# 在博客中加入新页面
在博客中加入新页面的方式有两种，一种是直接创建html文件，自己做一个网页，令一种是新建一个md格式的page，，最后考虑到博客的整体性，我选择了后者，下面是两种方法的具体过程
## 加入新html子页面
+ 首先，在博客根目录的source文件夹下，新建文件夹用于存放HTML文件

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/05/a19e058aacfc62f785cfd69176e78296.png)

hexo会对source文件夹中所有的页面进行渲染，所以我们自己的HTML文件需要跳过渲染。

+ 在博客根目录的配置文件_config.yml文件里，跳过渲染

    #跳过文件夹下所有文件
    skip_render: 
      - "文件夹名/*"  
## 新建一个page

cmd+win调出命令行，在博客对应目录输入

    hexo new page "页面名称"

hexo 会在source文件夹下创建一个对应的文件夹，里面有一个`index.md`的文件，在配置文件`_config.yml`中的`menu`下加入`/创建页面名称`，这样就创建好了新页面。


    # Header-菜单
    menu:
    Home: /
    Archives:  /archives/index.html
    Categories : /categories
    Knowledge nn : /nn
      
      
      
# Echart框架下载
第二步我们需要建立我们的神经图，这里我选择的JS的图表框架[Echart](https://echarts.apache.org/zh/index.html)，一个功能非常强大的框架，图表非常的美观
在这里我们总共需要两个js文件
+ echarts.min.js 主要的js文件，echart的压缩版本
  + 因为我们只用到关系图，所以也可以在官网通过定制只下载关系图的代码
+ jquery.js 当要用jquery调用json文件时加入

**下载地址**

**echarts.min.js**：https://echarts.apache.org/zh/download.html

**jquery.js**：http://blog.jquery.com/

也可以访问我的github直接下载所有源码文件
https://github.com/Fazziekey/Echart-nn


下载完成后将这两个文件放在Hexo\themes\<theme~name>\source\js下  

# Echart制作神经网络 


接下来在我们刚刚创建的md文件中直接插入下面的代码，我们需要给这个关系图提供一个容器

    <div id="main" style="width:100%;height:500px"></div> 
    <!--宽度推荐设置为100%占据整个网页-->
    <script src="echarts.min.js"></script>
    <script type="text/javascript"src="/js/jquery.js"></script>
    <!--如果不调用外部json文件可以删去-->
    <script type="text/javascript">

下面是如何配置神经网络图

----------------
    <div id="main" style="width:1000px;height:800px"></div>
    <script type="text/javascript">
        var myChart = echarts.init(document.getElementById('main'));
        var categories = [];   //设置图例标签
            categories[0] = {
                name: "Brain Center"
            };
    		categories[1] = {
                name: "工程"
            };
    		categories[2] = {
                name: "艺术"
            };
    		categories[3] = {
                name: "数理"
            };
    		categories[4] = {
                name: "逻辑"
            };
    		categories[5] = {
                name: "人文"
            };
    		categories[6] = {
                name: "社科"
            };
    		categories[7] = {
                name: "FCL"
            };
    
    		
        option = {
            // 图的标题
            title: {
                text: 'Learning Neural Network'
            },
            // 提示框的配置
            tooltip: {
                formatter: function (x) {
                    return x.data.des;
                }
            },
            // 工具箱
            toolbox: {
                // 显示工具箱
                show: true,
                feature: {
                    mark: {
                        show: true
                    },
                    // 还原
                    restore: {
                        show: true
                    },
                    // 保存为图片
                    saveAsImage: {
                        show: true
                    }
                }
            },
            legend: [{
                // selectedMode: 'single',
                data: categories.map(function (a) {
                    return a.name;
                })
            }],
            series: [{
                type: 'graph', // 类型:关系图
                layout: 'force', //图的布局，类型为力导图
                symbolSize: 40, // 调整节点的大小
                roam: true, // 是否开启鼠标缩放和平移漫游。默认不开启。如果只想要开启缩放或者平移,可以设置成 'scale' 或者 'move'。设置成 true 为都开启
                focusNodeAdjacency: true,   // 是否在鼠标移到节点上的时候突出显示节点以及节点的边和邻接节点。[ default: false ]
    	                force: {                // 力引导布局相关的配置项，力引导布局是模拟弹簧电荷模型在每两个节点之间添加一个斥力，每条边的两个节点之间添加一个引力，每次迭代节点会在各个斥力和引力的作用下移动位置，多次迭代后节点会静止在一个受力平衡的位置，达到整个模型的能量最小化。
    	                                // 力引导布局的结果有良好的对称性和局部聚合性，也比较美观。
    	            repulsion: 1000,            // [ default: 50 ]节点之间的斥力因子(关系对象之间的距离)。支持设置成数组表达斥力的范围，此时不同大小的值会线性映射到不同的斥力。值越大则斥力越大
    	            edgeLength: [150, 100]      // [ default: 30 ]边的两个节点之间的距离(关系对象连接线两端对象的距离,会根据关系对象值得大小来判断距离的大小)，
    	                                        // 这个距离也会受 repulsion。支持设置成数组表达边长的范围，此时不同大小的值会线性映射到不同的长度。值越小则长度越长。如下示例:
    	                                        // 值最大的边长度会趋向于 10，值最小的边长度会趋向于 50      edgeLength: [10, 50]
    	        },
    			edgeSymbol: ['circle', 'arrow'],
                edgeSymbolSize: [2, 10],
                edgeLabel: {
                    normal: {
                        textStyle: {
                            fontSize: 20
                        }
                    }
                },
                force: {
                    repulsion: 2500,
                    edgeLength: [10, 50]
                },
                draggable: true,
                lineStyle: {
                    normal: {
                        width: 2,               //线条宽度
                        color: '#4b565b',       //线条颜色
    					type: 'solid',          // 线的类型[ default: solid ]   'dashed'    'dotted'
    	                opacity: 0.5,           // 图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形。[ default: 0.5 ]
    	                curveness: 0.3          // 边的曲度，支持从 0 到 1 的值，值越大曲度越大。[ default: 0 ]
    
                    }
                },
                edgeLabel: {				    // 连接两个关系对象的线上的标签
                    normal: {
                        show: true,
                        formatter: function (x) {
                            return x.data.name;
                        }
                    }
                },
                label: {						//对象标签
                    normal: {
                        show: true,
                        textStyle: {}
                    }
                },
     
                // 数据
                data: [{
                    name: 'Brain Center',
                    des: 'nodedes01',
                    symbolSize: 100,
                    category: 0,
                }, {
                    name: '程序语言',
                    des: 'nodedes02',
                    symbolSize: 80,
                    category: 1,
                }, {
                    name: '音乐',
                    des: 'nodedes3',
                    symbolSize: 80,
                    category: 2,
                }, {
                    name: '课程',
                    des: 'nodedes04',
                    symbolSize: 80,
                    category: 7,
                }, {
                    name: '书籍',
                    des: 'nodedes05',
                    symbolSize: 80,
                    category: 7,
                }
    			],
    			//节点关系
                links: [{
                    source: '程序语言',
                    target: 'Brain Center',
                    name: 'Softmax',
                    des: 'link01des'
                }, {
                    source: '音乐',
                    target: 'Brain Center',
                    name: 'Softmax',
                    des: 'link02des'
                }, {
                    source: '课程',
                    target: 'Brain Center',
                    name: 'Softmax',
                    des: 'link03des'
                }, {
                    source: '书籍',
                    target: 'Brain Center',
                    name: 'Softmax',
                    des: 'link05des'
                }],
                categories: categories,
            }]
        };
        myChart.setOption(option);
    </script>
    </body>
</html>


## 最终效果

也可以直接访问我侧边栏的**Knowledge nn**



![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed@master/2020/08/08/af24bcbd2f1e99a78dca8b7228e0c9fc.png)