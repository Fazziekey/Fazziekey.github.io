---
title: Super Intelligence
date: 2020-08-08 00:16:05
type: "nn" 
---
# Super Intelligence :Fazzie
建这个Blog的最初目的是为了记录自己的深度学习的过程，有一天突发奇想能不能建立一个神经网络来记录自己的学习生活和人生经历，神经网络的思想来源于人的神经元，而人的生活就像神经网络一样，接受这外界的输入，通过一个个隐藏单元的激励函数，最后得到一个输出，通过不断训练去提高网络的性能。我把人的底层能力和知识体系分为，**工程技术**、**艺术设计**、**数理逻辑**、**视野格局**、**人文社科**、**沟通表达**六个层面，其他的中立性质的节点用全连接层（FCL）表示。希望自己保持终身学习，持续地对外输出独一无二的价值。

在这张神经网络计算图里，我将记录：
+ 学习生活
+ 有意义的经历
+ 所有喜欢的东西

如果你也想搭建自己的神经网络图谱，可以参考这篇文章

[建立你的知识神经网络](https://Fazziekey.github.io/2020/08/08/nn/)

The initial purpose of building this Blog is to record my own deep learning process. One day I suddenly thought that I could build a neural network to record my learning life and life experience. training to improve the performance of the network. I divide the underlying human ability and knowledge system into, **Engineering and Technology**, **Art and Design**, **Mathematical and Logical**, **Horizon and Perspective**, **Humanities and Society**, **Communication and Expression** six levels, and other nodes of a neutral nature are represented by the Fully Connected Layer (FCL). I hope to keep lifelong learning and export unique values to the world.

In this neural network computational map, I will record.
+ Learning experience and life
+ Everything Meaningful
+ Anything I love

If you also want to build your own neural network graph, you can refer to this article

[Build your own neural network](https://Fazziekey.github.io/2020/08/08/nn/)

----------------------------

<div id="nn" style="width:100%;height:800px;"></div>
<script type="text/javascript"src="/js/echarts.min.js"></script>
<script type="text/javascript"src="/js/jquery.js"></script>
<script type="text/javascript">
    var myChart = echarts.init(document.getElementById('nn'));

	$.getJSON('./data.json', function (data) {
		myChart.hideLoading();
		var categories = [];   //标签
			categories[0] = {name: "Neural Center"};
			categories[1] = {name: "工程技术"};
			categories[2] = {name: "艺术设计"};
			categories[3] = {name: "数理逻辑"};
			categories[4] = {name: "视野格局"};
			categories[5] = {name: "人文社科"};
			categories[6] = {name: "沟通表达"};
			categories[7] = {name: "FCL"};

		option = {
			// 图的标题
			title: {
				text: ''
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
				data: data.data,
        		links: data.links,
				categories: categories,
			}]
		};
		myChart.setOption(option);

	});


</script>