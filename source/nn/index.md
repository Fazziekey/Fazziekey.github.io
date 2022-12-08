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
 
            // 数据
            data: [
				{name: 'Neural Center', symbolSize: 200,category: 0,},
				 	{name: '程序语言', symbolSize: 60,category: 1,},
						{name: 'Python', symbolSize: 30,category: 1,}, 
							{name: '网络爬虫', symbolSize: 10,category: 1,}, 
						{name: 'C', symbolSize: 30,category: 1,},
						{name: 'C++', symbolSize: 30,category: 1,},
						{name: 'Go', symbolSize: 20,category: 1,},
							{name: 'OpenCL', symbolSize: 10,category: 1,},
						{name: 'Verilog', symbolSize: 30,category: 1,},
							{name: 'Modelsim', symbolSize: 10,category: 1,},
							{name: 'Vivado', symbolSize: 10,category: 1,},
						{name: 'Matlab', symbolSize: 30,category: 1,},
						{name: 'JavaScript', symbolSize: 30,category: 1,},
						{name: 'CSS', symbolSize: 30,category: 1,},
						{name: 'html', symbolSize: 30,category: 1,},
						{name: 'Dart', symbolSize: 30,category: 1,},
						{name: 'java', symbolSize: 10,category: 1,},
						{name: 'C#', symbolSize: 10,category: 1,},
					{name: '算法工程师的吊灯', symbolSize: 60,category: 1,},
					{name: '音乐', symbolSize: 100,category: 2,},
						{name: '电子', symbolSize: 60,category: 2,},
							{name: 'Progressive house', symbolSize: 10,category: 2,},
							{name: 'Future house', symbolSize: 10,category: 2,},
							{name: 'Melodic dubstep', symbolSize: 10,category: 2,},
							{name: 'Future Bass', symbolSize: 10,category: 2,},
							{name: 'Tropical house', symbolSize: 10,category: 2,},
						{name: '摇滚', symbolSize: 30,category: 2,},
						{name: '金属', symbolSize: 30,category: 2,},
						{name: 'Ableton live', symbolSize: 20,category: 2,},
						{name: 'Fl studio', symbolSize: 10,category: 2,},
						{name: 'Traktor', symbolSize: 10,category: 2,},
						{name: 'Launchpad', symbolSize: 20,category: 2,},
						{name: '架子鼓', symbolSize: 60,category: 2,},
					{name: '终身学习', symbolSize: 150,category: 7,}, 
						{name: '体育', symbolSize: 30,category: 7,},
							{name: '足球', symbolSize: 10,category: 7,},
							{name: '网球', symbolSize: 10,category: 7,},
							{name: '赛艇', symbolSize: 10,category: 7,},
						{name: '通识', symbolSize: 60,category: 7,},
							{name: '画法几何', symbolSize:10,category: 2,},
							{name: '工程图学', symbolSize:10,category: 1,},
							{name: '经济法', symbolSize:10,category: 5,},
							{name: '法学基础', symbolSize:10,category: 5,},
							{name: '公共经济分析', symbolSize:10,category: 5,},
							{name: '中国土地制度', symbolSize:10,category: 5,},
							{name: '视唱练耳', symbolSize:10,category: 2,},
							{name: '数字电视', symbolSize:10,category: 1,},
						{name: 'EE', symbolSize: 100,category: 1,},
							{name: 'Arduino', symbolSize: 10,category: 1,},
							{name: '电子工程训练', symbolSize: 10,category: 1,},
							{name: '信电导论', symbolSize: 10,category: 1,},
							{name: '电子电路基础', symbolSize: 10,category: 1,},
							{name: '信号与系统', symbolSize: 30,category: 1,},
							{name: '数字电路', symbolSize: 30,category: 1,},
							{name: '电子电路实验', symbolSize: 10,category: 1,},
							{name: 'Wireless and Lot', symbolSize: 10,category: 1,},
							{name: 'Wierless Communication', symbolSize: 10,category: 1,},
							{name: '电磁场与电池波', symbolSize: 30,category: 1,},
							{name: '射频电路', symbolSize: 10,category: 1,},
							{name: '信息电子物理', symbolSize: 10,category: 1,},
							{name: '信息论', symbolSize: 10,category: 1,},
						{name: 'CS', symbolSize: 100,category: 1,},
							{name: 'Linux', symbolSize: 10,category: 1,},
							{name: '软件技术基础', symbolSize:10,category: 1,},
							{name: '深度学习', symbolSize:30,category: 1,},
							{name: '计算机网络', symbolSize:10,category: 1,},
							{name: '操作系统', symbolSize:10,category: 1,},
							{name: '数据库', symbolSize:10,category: 1,},
							{name: '数据挖掘', symbolSize:10,category: 1,},
								{name: 'pytorch', symbolSize:10,category: 1,},
								{name: 'Mindspore', symbolSize:10,category: 1,},
							{name: '机器学习和机器视觉', symbolSize:10,category: 1,},
							{name: '分布式机器学习', symbolSize:10,category: 1,},
							{name: '强化学习', symbolSize:10,category: 1,},
							{name: '边缘计算', symbolSize:10,category: 1,},
							{name: '数据分析与算法设计', symbolSize:10,category: 1,},
							{name: '计算机组成', symbolSize:10,category: 1,},
						{name: '数学', symbolSize: 60,category: 3,},
							{name: '微积分', symbolSize: 30,category: 3,},
							{name: '线性代数', symbolSize: 30,category: 3,},
							{name: '常微分', symbolSize: 10,category: 3,},
							{name: '复变函数', symbolSize: 10,category: 3,},
							{name: '概率统计', symbolSize: 20,category: 3,},
							{name: '矩阵论', symbolSize: 10,category: 3,},
							{name: '离散数学', symbolSize: 10,category: 3,},
						{name: '物理', symbolSize: 60,category: 3,},
							{name: '大学物理', symbolSize: 30,category: 3,},
							{name: '大学物理实验', symbolSize: 10,category: 3,},
						{name: 'ITP课程', symbolSize: 100,category: 7,},
							{name: '管理学', symbolSize: 10,category: 5,},
							{name: '团队沟通与领导力', symbolSize: 10,category: 6,},
							{name: '创业战略', symbolSize: 10,category: 4,},
							{name: '经济学', symbolSize: 10,category: 5,},
							{name: '商业模式', symbolSize: 10,category: 5,},
							{name: '市场营销', symbolSize: 10,category: 5,},
							{name: '项目管理', symbolSize: 10,category: 5,},
							{name: '市场调研', symbolSize: 10,category: 5,},
							{name: '创业财务', symbolSize: 10,category: 5,},
							{name: '创业法务', symbolSize: 10,category: 5,},
							{name: '创业融资与估值', symbolSize: 10,category: 5,},
					{name: '读万卷书', symbolSize: 100,category: 7,},
						{name: '科幻', symbolSize: 40,category: 1,},
							{name: '《三体》', symbolSize: 10,category: 1,},
							{name: '《银河之心》', symbolSize: 10,category: 1,},
							{name: '《球状闪电》', symbolSize: 10,category: 1,},
							{name: '《银河帝国》', symbolSize: 10,category: 1,},
							{name: '《银河英雄传说》', symbolSize: 10,category: 1,},
						{name: '历史', symbolSize: 40,category: 7,},
							{name: '《全球通史》', symbolSize: 10,category: 5,},
							{name: '《人类简史》', symbolSize: 10,category: 5,},
							{name: '《未来简史》', symbolSize: 10,category: 5,},
							{name: '《今日简史》', symbolSize: 10,category: 5,},
							{name: '《世界秩序》', symbolSize: 10,category: 5,},
							{name: '《枢纽》', symbolSize: 10,category: 5,},
							{name: '《三国志》', symbolSize: 10,category: 5,},
							{name: '《刺客信条》', symbolSize: 10,category: 5,},
						{name: '科学', symbolSize: 40,category: 7,},
							{name: '《生命3.0》', symbolSize: 10,category: 3,},
							{name: '《思维简史》', symbolSize: 10,category: 3,},
							{name: '《数学之美》', symbolSize: 10,category: 3,},
						{name: '思维', symbolSize: 40,category: 7,},
							{name: '《学会提问》', symbolSize: 10,category: 3,},
							{name: '《金字塔原理》', symbolSize: 10,category: 3,},
							{name: '《智识分子》', symbolSize: 10,category: 3,},
							{name: '《万万没想到》', symbolSize: 10,category: 3,},
							{name: '《孙子兵法》', symbolSize: 10,category: 3,},
						{name: '创业', symbolSize: 40,category: 4,},
							{name: '《激荡30年》', symbolSize: 10,category: 4,},
							{name: '《从0到1》', symbolSize: 10,category: 4,},
							{name: '《腾讯传》', symbolSize: 10,category: 4,},
							{name: '《智能时代》', symbolSize: 10,category: 4,},
							{name: '《海底捞你学不会》', symbolSize: 10,category: 4,},
							{name: '《创新者的窘境》', symbolSize: 10,category: 4,},
					{name: '行万里路', symbolSize: 100,category: 4,},
							{name: '北京', symbolSize: 10,category: 4,},
							{name: '青岛', symbolSize: 10,category: 4,},
							{name: '上海', symbolSize: 10,category: 4,},
							{name: '西双版纳', symbolSize: 10,category: 4,},
							{name: '南京', symbolSize: 10,category: 4,},
							{name: '宁波', symbolSize: 10,category: 4,},
							{name: '舟山', symbolSize: 10,category: 4,},
							{name: '洛阳', symbolSize: 10,category: 4,},
							{name: '海南', symbolSize: 10,category: 4,},
							{name: '黄山', symbolSize: 10,category: 4,},
							{name: '香港', symbolSize: 10,category: 4,},
							{name: '安吉', symbolSize: 10,category: 4,},
						{name: '韩国', symbolSize: 30,category: 4,},
							{name: '首尔', symbolSize: 10,category: 4,},
							{name: '釜山', symbolSize: 10,category: 4,},
						{name: 'America', symbolSize: 60,category: 4,},
							{name: 'New York', symbolSize: 10,category: 4,},
							{name: 'Philadelphia', symbolSize: 10,category: 4,},
							{name: 'San Francisco', symbolSize: 10,category: 4,},
							{name: 'Los Angeles', symbolSize: 10,category: 4,},
							{name: 'Washington', symbolSize: 10,category: 4,},
							{name: 'Boston', symbolSize: 10,category: 4,},
						{name: '新加坡', symbolSize: 30,category: 4,},
					{name: '科研之路', symbolSize: 100,category: 7,},
						{name: '香农班', symbolSize: 80,category: 7,},
							{name: 'mmwave&DL课题调研', symbolSize: 20,category: 1,},
						{name: 'SRTP', symbolSize: 50,category: 1,},
					{name: 'ZJU life', symbolSize: 120,category: 7,},
						{name: 'Six o\'clock studio', symbolSize: 80,category: 2,},
							{name: '新生达人秀', symbolSize: 10,category: 2,},
							{name: '求是新晚', symbolSize: 10,category: 2,},
							{name: '秋声音乐节', symbolSize: 10,category: 2,},
							{name: '棉花糖音乐节', symbolSize: 10,category: 2,},
							{name: '信电新晚', symbolSize: 10,category: 2,},
							{name: '石榴音乐节', symbolSize: 10,category: 2,},
							{name: '云峰音乐节', symbolSize: 10,category: 2,},
							{name: '葫芦音乐节', symbolSize: 10,category: 2,},
						{name: '勤创', symbolSize: 80,category: 6,},
							{name: '创业论坛', symbolSize: 10,category: 6,},
							{name: '创指三面', symbolSize: 10,category: 6,},
							{name: '走进名企', symbolSize: 10,category: 6,},
							{name: '精英团队挑战赛', symbolSize: 20,category: 6,},
							{name: '秋纳', symbolSize: 10,category: 6,},
							{name: '春纳', symbolSize: 10,category: 6,},
							{name: '创指部长团', symbolSize: 30,category: 6,},
							{name: '名家讲坛', symbolSize: 10,category: 6,},
						{name: '洛阳支教', symbolSize: 30,category: 6,},
						{name: 'UIUC交流', symbolSize: 30,category: 1,},
						{name: '新加坡交流', symbolSize: 30,category: 4,},
					{name: '梦与追求', symbolSize: 120,category: 7,},
						{name: '开班仪式', symbolSize: 20,category: 4,},
						{name: '19招生', symbolSize: 20,category: 4,},
					{name: '网瘾少年', symbolSize: 80,category: 7,},
						{name: '守望先锋', symbolSize: 10,category: 1,},
						{name: '英雄联盟', symbolSize: 10,category: 1,},
						{name: '星际争霸', symbolSize: 10,category: 1,},
						{name: '风暴英雄', symbolSize: 10,category: 1,},
						{name: '炉石传说', symbolSize: 10,category: 3,},
						{name: '绝地求生', symbolSize: 10,category: 1,},
						{name: '彩虹六号', symbolSize: 10,category: 1,},
						{name: '泰坦陨落', symbolSize: 10,category: 1,},
						{name: '看门狗', symbolSize: 10,category: 1,},
						{name: '巫师三', symbolSize: 10,category: 5,},
						{name: '生化奇兵', symbolSize: 10,category: 1,},
						{name: '戴森球计划', symbolSize: 10,category: 1,},
						{name: '文明6', symbolSize: 10,category: 5,},
						{name: '2077', symbolSize: 10,category: 5,},
						{name: 'Assassin Creed', symbolSize: 60,category: 5,},
							{name: '刺客信条2', symbolSize: 10,category: 5,},
							{name: '刺客信条3', symbolSize: 10,category: 5,},
							{name: '大革命', symbolSize: 10,category: 5,},
							{name: '枭雄', symbolSize: 10,category: 5,},
							{name: '奥德赛', symbolSize: 10,category: 5,},
							{name: '起源', symbolSize: 10,category: 5,},
							{name: '英灵殿', symbolSize: 10,category: 5,},
				{name: '打工人打工魂', symbolSize: 60,category: 7},
					{name: '华为2012', symbolSize: 30,category: 7},
			],
			//节点关系
            links: [
				{source: '程序语言',target: 'Neural Center',name: 'Softmax'}, 
				{source: '算法工程师的吊灯',target: 'Neural Center',name: 'Softmax'}, 
				{source: 'CS',target: 'Neural Center',name: 'Softmax'}, 
					{source: 'Python',target: '程序语言',name:  'Relu'},
						{source: 'Python',target: '算法工程师的吊灯',name:  'Relu'},
						{source: 'Python',target: '深度学习',name:  'Relu'},
						{source: '网络爬虫',target: 'Python',name:  'Relu'},
					{source: 'C',target: '程序语言',name:  'Relu'},
					{source: 'C++',target: '程序语言',name:  'Relu'},
						{source: 'OpenCL',target: 'C++',name:  'Relu'},
					{source: 'C++',target: '算法工程师的吊灯',name:  'Relu'},
					{source: 'Verilog',target: '程序语言',name:  'Relu'},
					{source: 'Modelsim',target: 'Verilog',name:  'Relu'},
						{source: 'Vivado',target: 'Verilog',name:  'Relu'},
						{source: 'Matlab',target: '程序语言',name:  'Relu'},
					{source: 'Go',target: '程序语言',name:  'Relu'},
					{source: 'CSS',target: '程序语言',name:  'Relu'},
					{source: 'html',target: '程序语言',name:  'Relu'},
					{source: 'JavaScript',target: '程序语言',name:  'Relu'},
					{source: 'Dart',target: '程序语言',name:  'Relu'},
					{source: 'java',target: '程序语言',name:  'Relu'},
					{source: 'C#',target: '程序语言',name:  'Relu'},
				{source: '音乐',target: 'Neural Center',name: 'Softmax', },
					{source: '电子',target: '音乐',name: 'Conv'},
						{source: 'Progressive house',target: '电子',name: 'Conv'},
						{source: 'Tropical house',target: '电子',name: 'Conv'},
						{source: 'Future house',target: '电子',name: 'Conv'},
						{source: 'Melodic dubstep',target: '电子',name: 'Conv'},
						{source: 'Future Bass',target: '电子',name: 'Conv'},
					{source: '摇滚',target: '音乐',name: 'Conv'},
					{source: '金属',target: '音乐',name: 'Conv'},
					{source: '架子鼓',target: '音乐',name: 'Conv'},
					{source: 'Ableton live',target: '音乐',name: 'Conv'},
					{source: 'Fl studio',target: '音乐',name: 'Conv'},
					{source: 'Traktor',target: '音乐',name: 'Conv'},
					{source: 'Launchpad',target: '音乐',name: 'Conv'},
			 	{source: '终身学习',target: 'Neural Center',name: 'Softmax' }, 
				 	{source: '体育',target: '终身学习',name: 'Softmax' },
						{source: '足球',target: '体育',name: 'Conv' },
						{source: '网球',target: '体育',name: 'Conv' },
						{source: '赛艇',target: '体育',name: 'Conv' },
					{source: '通识',target: '终身学习',name: 'Softmax' },
					 	 {source: '画法几何',target: '通识',name: 'Relu' },
						 {source: '工程图学',target: '通识',name: 'Relu' },
						 {source: '经济法',target: '通识',name: 'Relu' },
						 {source: '法学基础',target: '通识',name: 'Relu' },
						 {source: '公共经济分析',target: '通识',name: 'Relu' },
						 {source: '中国土地制度',target: '通识',name: 'Relu' },
						 {source: '视唱练耳',target: '通识',name: 'Relu' },
						 {source: '视唱练耳',target: '音乐',name: 'Relu' },
						 {source: '数字电视',target: '通识',name: 'Relu' },
				 	{source: 'EE',target: '终身学习',name: 'Softmax' },
					{source: 'CS',target: '终身学习',name: 'Softmax' },
					{source: 'EE',target: 'Neural Center',name: 'Softmax' },
						{source: 'Arduino',target: 'EE',name: 'Relu' },
						{source: '电子工程训练',target: 'EE',name: 'Relu' },
						{source: '信电导论',target: 'EE',name: 'Relu' },
						{source: '信电导论',target: 'Matlab',name: 'Relu' },
						{source: '电子电路基础',target: 'EE',name: 'Relu' },
						{source: '信号与系统',target: 'EE',name: 'Relu' },
						{source: '信号与系统',target: '数学',name: 'Relu' },
						{source: '信号与系统',target: 'Matlab',name: 'Relu' },
						{source: '数字电路',target: 'EE',name: 'Relu' },
						{source: '数字电路',target: 'Verilog',name: 'Relu' },
						{source: '电子电路实验',target: 'EE',name: 'Relu' },
						{source: '电子电路实验',target: 'Arduino',name: 'Relu' },
						{source: 'Wireless and Lot',target: 'EE',name: 'Relu' },
						{source: 'Wierless Communication',target: 'EE',name: 'Relu' },
						{source: '电磁场与电池波',target: 'EE',name: 'Relu' },
						{source: '电磁场与电池波',target: '物理',name: 'Relu' },
						{source: '信息电子物理',target: '物理',name: 'Relu' },
						{source: '信息电子物理',target: 'EE',name: 'Relu' },
						{source: '信息论',target: 'EE',name: 'Relu' },
						{source: '射频电路',target: 'EE',name: 'Relu' },
					{source: 'CS',target: 'Neural Center',name: 'Softmax' },
						 {source: 'Linux',target: 'CS',name: 'Relu' },
						 {source: 'C',target: 'CS',name: 'Relu' },
						 {source: '软件技术基础',target: 'CS',name: 'Relu' },
						 {source: '操作系统',target: 'CS',name: 'Relu' },
						 {source: '计算机网络',target: 'CS',name: 'Relu' },
						 {source: '数据库',target: 'CS',name: 'Relu' },
						 {source: '数据挖掘',target: 'CS',name: 'Relu' },
						 {source: 'Python',target: 'CS',name: 'Relu' },
						 {source: '深度学习',target: 'CS',name: 'Relu' },
						 {source: '深度学习',target: '算法工程师的吊灯',name: 'Relu' },
						 	{source: '深度学习',target: 'SRTP',name: 'Relu' },
						 	{source: 'pytorch',target: '深度学习',name: 'Relu' },
							{source: 'pytorch',target: '算法工程师的吊灯',name: 'Relu' },
							{source: 'Mindspore',target: '深度学习',name: 'Relu' },
							{source: 'Mindspore',target: '华为2012',name: 'self-attention' },
							{source: 'Mindspore',target: '算法工程师的吊灯',name: 'Relu' },
							{source: '分布式机器学习',target: '算法工程师的吊灯',name: 'Relu' },
							{source: '分布式机器学习',target: '华为2012',name: 'self-attention' },
						 	{source: 'pytorch',target: 'Python',name: 'Relu' },
						 {source: '机器学习和机器视觉',target: 'CS',name: 'Relu' },
						 {source: '强化学习',target: '算法工程师的吊灯',name: 'Relu' },
						 {source: '机器学习和机器视觉',target: '算法工程师的吊灯',name: 'Relu' },
						 {source: '强化学习',target: 'CS',name: 'Relu' },
						 {source: '计算机组成',target: 'CS',name: 'Relu' },
						 {source: '计算机组成',target: 'EE',name: 'Relu' },
						 {source: '边缘计算',target: 'CS',name: 'Relu' },
						 {source: '边缘计算',target: 'EE',name: 'Relu' },
						 {source: '数据分析与算法设计',target: 'CS',name: 'Relu' },
					{source: '数学',target: '终身学习',name: 'Softmax' }, 
						{source: '微积分',target: '数学',name: 'tanh' }, 
						{source: '线性代数',target: '数学',name: 'tanh' }, 
						{source: '常微分',target: '数学',name: 'tanh' }, 
						{source: '概率统计',target: '数学',name: 'tanh' }, 
						{source: '复变函数',target: '数学',name: 'tanh' }, 
						{source: '离散数学',target: '数学',name: 'tanh' }, 
						{source: '矩阵论',target: '数学',name: 'tanh' }, 
					{source: '物理',target: '终身学习',name: 'Softmax' },
						{source: '大学物理',target: '物理',name: 'tanh' },
						{source: '大学物理实验',target: '物理',name: 'tanh' }, 
					{source: 'ITP课程',target: '终身学习',name: 'Softmax' },
					{source: 'ITP课程',target: '梦与追求',name: 'Softmax' },
						{source: '管理学',target: 'ITP课程',name: 'tanh' },
						{source: '团队沟通与领导力',target: 'ITP课程',name: 'tanh' }, 
						{source: '经济学',target: 'ITP课程',name: 'tanh' }, 
						{source: '创业战略',target: 'ITP课程',name: 'tanh' },  
						{source: '商业模式',target: 'ITP课程',name: 'tanh' },  
						{source: '市场营销',target: 'ITP课程',name: 'tanh' },  
						{source: '项目管理',target: 'ITP课程',name: 'tanh' },  
						{source: '市场调研',target: 'ITP课程',name: 'tanh' }, 
						{source: '创业法务',target: 'ITP课程',name: 'tanh' },  
						{source: '创业财务',target: 'ITP课程',name: 'tanh' },   
						{source: '创业融资与估值',target: 'ITP课程',name: 'tanh' },  
				{source: '读万卷书',target: 'Neural Center',name: 'Softmax' },
					{source: '科幻',target: '读万卷书',name: 'Pooling' },
						{source: '《三体》',target: '科幻',name: 'tanh' },
						{source: '《银河之心》',target: '科幻',name: 'tanh' },
						{source: '《球状闪电》',target: '科幻',name: 'tanh' },
						{source: '《银河帝国》',target: '科幻',name: 'tanh' },
						{source: '《银河英雄传说》',target: '科幻',name: 'tanh' },
					{source: '历史',target: '读万卷书',name: 'Pooling' },
						{source: '《全球通史》',target: '历史',name: 'tanh' },
						{source: '《人类简史》',target: '历史',name: 'tanh' },
						{source: '《未来简史》',target: '历史',name: 'tanh' },
						{source: '《今日简史》',target: '历史',name: 'tanh' },
						{source: '《世界秩序》',target: '历史',name: 'tanh' },
						{source: '《枢纽》', target: '历史',name: 'tanh'},
						{source: '《三国志》', target: '历史',name: 'tanh'},
						{source: '《刺客信条》', target: '历史',name: 'tanh'},
					{source: '科学',target: '读万卷书',name: 'Pooling' },
						{source: '《生命3.0》', target: '科学',name: 'tanh'},
						{source: '《思维简史》', target: '科学',name: 'tanh'},
						{source: '《数学之美》',target: '科学',name: 'tanh'},
					{source: '思维',target: '读万卷书',name: 'Pooling' },
						{source: '《学会提问》',target: '思维',name: 'tanh'},
						{source: '《金字塔原理》',target: '思维',name: 'tanh'},
						{source: '《智识分子》',target: '思维',name: 'tanh'},
						{source: '《万万没想到》',target: '思维',name: 'tanh'},
						{source: '《孙子兵法》',target: '思维',name: 'tanh'},
					{source: '创业',target: '读万卷书',name: 'Pooling' },
						{source: '《激荡30年》',target: '创业',name: 'tanh'},
						{source: '《从0到1》',target: '创业',name: 'tanh'},
						{source: '《腾讯传》',target: '创业',name: 'tanh'},
						{source: '《智能时代》',target: '创业',name: 'tanh'},
						{source: '《海底捞你学不会》',target: '创业',name: 'tanh'},
						{source: '《创新者的窘境》',target: '创业',name: 'tanh'},
				{source: '行万里路',target: 'Neural Center',name: 'Softmax' },
					{source: '北京',target: '行万里路',name: 'tanh'},
					{source: '青岛',target: '行万里路',name: 'tanh'},
					{source: '上海',target: '行万里路',name: 'tanh'},
					{source: '西双版纳',target: '行万里路',name: 'tanh'},
					{source: '南京',target: '行万里路',name: 'tanh'},
					{source: '宁波',target: '行万里路',name: 'tanh'},
					{source: '舟山',target: '行万里路',name: 'tanh'},
					{source: '洛阳',target: '行万里路',name: 'tanh'},
					{source: '海南',target: '行万里路',name: 'tanh'},
					{source: '黄山',target: '行万里路',name: 'tanh'},
					{source: '香港',target: '行万里路',name: 'tanh'},
					{source: '安吉',target: '行万里路',name: 'tanh'},
				{source: '韩国', target: '行万里路',name: 'tanh'},
					{source: '首尔',target: '韩国',name: 'tanh'},
					{source: '釜山',target: '韩国',name: 'tanh'},
				{source: 'America',target: '行万里路',name: 'tanh'},
					{source: 'New York',target: 'America',name: 'tanh'},
					{source: 'Philadelphia',target: 'America',name: 'tanh'},
					{source: 'San Francisco',target: 'America',name: 'tanh'},
					{source: 'Los Angeles',target: 'America',name: 'tanh'},
					{source: 'Washington',target: 'America',name: 'tanh'},
					{source: 'Boston', target: 'America',name: 'tanh'},
				{source: '新加坡',target: '行万里路',name: 'tanh'},
				{source: '科研之路',target: 'Neural Center',name: 'Softmax' },
					{source: '香农班',target: '科研之路',name: 'Softmax' },
						{source: 'mmwave&DL课题调研',target: '科研之路',name: 'Relu' },
					{source: 'SRTP',target: '科研之路',name: 'Softmax' },
				{source: 'ZJU life',target: 'Neural Center',name: 'Softmax' },
					{source: 'Six o\'clock studio',target: 'ZJU life',name: 'Pooling'},
					{source: 'Six o\'clock studio',target: '音乐',name: 'Pooling'},
						{source: '新生达人秀',target: 'Six o\'clock studio',name: 'Conv'},
						{source: '石榴音乐节',target: 'Six o\'clock studio',name: 'Conv'},
						{source: '棉花糖音乐节',target: 'Six o\'clock studio',name: 'Conv'},
						{source: '云峰音乐节',target: 'Six o\'clock studio',name: 'Conv'},
						{source: '求是新晚',target: 'Six o\'clock studio',name: 'Conv'},
						{source: '信电新晚',target: 'Six o\'clock studio',name: 'Conv'},
						{source: '秋声音乐节',target: 'Six o\'clock studio',name: 'Conv'},
						{source: '葫芦音乐节',target: 'Six o\'clock studio',name: 'Conv'},
					{source: '勤创',target: 'ZJU life',name: 'Pooling'},
						{source: '春纳',target: '勤创',name: 'Conv'},
						{source: '创指三面',target: '勤创',name: 'Conv'},
						{source: '秋纳',target: '勤创',name: 'Conv'},
						{source: '走进名企',target: '勤创',name: 'Conv'},
						{source: '创业论坛',target: '勤创',name: 'Conv'},
						{source: '精英团队挑战赛',target: '勤创',name: 'Conv'},
						{source: '创指部长团',target: '勤创',name: 'Conv'},
						{source: '名家讲坛',target: '勤创',name: 'Conv'},
					{source: '洛阳支教',target: 'ZJU life',name: 'Pooling'},
					{source: '洛阳支教',target: '洛阳',name: 'Pooling'},
					{source: '新加坡交流',target: 'ZJU life',name: 'Pooling'},
					{source: '新加坡交流',target: '新加坡',name: 'Pooling'},
					{source: 'UIUC交流',target: 'ZJU life',name: 'Pooling'},
				{source: '梦与追求',target: 'Neural Center',name: 'Softmax' },
					{source: '开班仪式',target: '梦与追求',name: 'Softmax' },
					{source: '19招生',target: '梦与追求',name: 'Softmax' },
				{source: '网瘾少年',target: 'Neural Center',name: 'Softmax' },
					{source: '守望先锋',target: '网瘾少年',name: 'Sigmod' },
					{source: '英雄联盟',target: '网瘾少年',name: 'Sigmod' },
					{source: '星际争霸',target: '网瘾少年',name: 'Sigmod' },
					{source: '炉石传说',target: '网瘾少年',name: 'Sigmod' },
					{source: '风暴英雄',target: '网瘾少年',name: 'Sigmod' },
					{source: '绝地求生',target: '网瘾少年',name: 'Sigmod' },
					{source: '彩虹六号',target: '网瘾少年',name: 'Sigmod' },
					{source: '泰坦陨落',target: '网瘾少年',name: 'Sigmod' },
					{source: '看门狗',target: '网瘾少年',name: 'Sigmod' },
					{source: '戴森球计划',target: '网瘾少年',name: 'Sigmod' },
					{source: '巫师三',target: '网瘾少年',name: 'Sigmod' },
					{source: '生化奇兵',target: '网瘾少年',name: 'Sigmod' },
					{source: '文明6',target: '网瘾少年',name: 'Sigmod' },
					{source: '2077',target: '网瘾少年',name: 'Sigmod' },
					{source: 'Assassin Creed',target: '网瘾少年',name: 'Sigmod' },
						{source: '刺客信条2',target: 'Assassin Creed',name: 'Sigmod' },
						{source: '刺客信条3',target: 'Assassin Creed',name: 'Sigmod' },
						{source: '大革命',target: 'Assassin Creed',name: 'Sigmod' },
						{source: '枭雄',target: 'Assassin Creed',name: 'Sigmod' },
						{source: '奥德赛',target: 'Assassin Creed',name: 'Sigmod' },
						{source: '起源',target: 'Assassin Creed',name: 'Sigmod' },
						{source: '英灵殿',target: 'Assassin Creed',name: 'Sigmod' },
				{source: '打工人打工魂', target: 'Neural Center', name: 'Softmax'},
					{source: '华为2012', target: '打工人打工魂', name: 'self-attention'},
			],
            categories: categories,
        }]
    };
    myChart.setOption(option);
</script>