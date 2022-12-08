---
title: 蒙特卡洛搜索实现黑白棋
toc: true
copyright: true
date: 2021-05-10 22:31:44
tags:
    - Monte Carlo search
categories:
    - 《炼金术士修炼手册》
reward:
---

# 问题重述
## 黑白棋简介

黑白棋(Reversi),也叫翻转棋，是一款经典的策略游戏。

一般棋子双面为黑白两色，故称“黑白棋”。因为行棋之时将对方棋子翻转，则变为己方棋子，故又称“翻转棋” (Reversi) 。

它使用 8x8 的棋盘，由两人执黑子和白子轮流下棋，最后子多方为胜方。

### 游戏规则
开始时，黑棋位于D5和E4,白棋位于D4和E5.
一个合法的落子：

+ 在空处落子、并翻转对手一个或多个棋子
+ 新落子位置必须在可以夹住对方的位置上、对方被夹住的棋子翻转。可以是横着夹、竖着夹、对角线夹
+ 任何被夹住的棋子必须被反过来
如果一方没有合法棋步，也就是无论他下在哪里，都无法翻转对方的棋子了，这一轮只能弃权
棋局持续知道棋盘填满或双方都没有合法棋步可下
如果一方落子时间超过1min，或者连续三次落子不合法，则判断该方失败


## 棋盘类介绍


###  初始化棋盘



棋盘规格是 8x8，'X' 代表黑棋，'O' 代表白棋，'.' 代表未落子状态。
  
棋盘初始化 - 利用 Board 类（board.py）中的 `display()` 方法展示棋盘：



### 导入棋盘文件
    from board import Board

#### 初始化棋盘
board = Board()

# 打印初始化棋盘
    board.display()


### 棋盘与坐标之间的关系    

||A|B|C|D|E|F|G|H|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|1|(0,0)|(0,1)|(0,2)|(0,3)|(0,4)|(0,5)|(0,6)|(0,7)|
|2|(1,0)|(1,1)|(1,2)|(1,3)|(1,4)|(1,5)|(1,6)|(1,7)|
|3|(2,0)|(2,1)|(2,2)|(2,3)|(2,4)|(2,5)|(2,6)|(2,7)|
|4|(3,0)|(3,1)|(3,2)|(3,3)|(3,4)|(3,5)|(3,6)|(3,7)|
|5|(4,0)|(4,1)|(4,2)|(4,3)|(4,4)|(4,5)|(4,6)|(4,7)|
|6|(5,0)|(5,1)|(5,2)|(5,3)|(5,4)|(5,5)|(5,6)|(5,7)|
|7|(6,0)|(6,1)|(6,2)|(6,3)|(6,4)|(6,5)|(6,6)|(6,7)|
|8|(7,0)|(7,1)|(7,2)|(7,3)|(7,4)|(7,5)|(7,6)|(7,7)|



棋盘坐标 E4, 转化为坐标形式就是 (3, 4), 坐标数值大小是从 0 开始，到 7 结束。  

Board 类中，提供以上两种坐标的转化方法：
+ `board_num(action)`: 棋盘坐标转化为数字坐标。
    + action: 棋盘坐标，e.g. 'G6'
    + 返回值: 数字坐标，e.g. (5, 6)
+ `num_board(action)`: 数字坐标转化为棋盘坐标。
    + action: 数字坐标，e.g. (2, 7)
    + 返回值: 棋盘坐标，e.g. 'H3'



### 查看坐标 (4,3) 在棋盘上的位置 
    position = (4, 3)
    print(board.num_board(position))

### 查看棋盘位置 'G2' 的坐标
    position = 'G2'
    print(board.board_num(position))


### Board 类中比较重要的方法


+ `get_legal_actions(color)`： 根据黑白棋的规则获取 color 方棋子的合法落子坐标，用 `list()` 方法可以获取所有的合法坐标。
    + color: 下棋方，'X' - 黑棋，'O' - 白棋
    + 返回值: 合法的落子坐标列表  


### 棋盘初始化后，黑方可以落子的位置
    print(list(board.get_legal_actions('X')))



  
+  `_move(action, color)`：  根据 color 落子坐标 action 获取翻转棋子的坐标。  
    + action: 落子的坐标，e.g. 'C4'
    + color: 下棋方，'X' - 黑棋，'O' - 白棋
    + 返回值: 反转棋子棋盘坐标列表



### 打印初始化后的棋盘
    board.display()

#### 假设现在黑棋下棋，可以落子的位置有：['D3', 'C4', 'F5', 'E6']，
#### 黑棋落子 D3 , 则白棋被翻转的棋子是 D4。 

#### 表示黑棋
    color = 'X' 

#### 落子坐标
    action = 'D3' 

### 打印白方被翻转的棋子位置
    print(board._move(action,color))

### 打印棋盘
    board.display()


## Game 类

该类主要实现黑白棋的对弈，已经实现随机玩家和人类玩家，现在可以来对弈一下。    
Game 类（game.py）的主要方法和属性:  

+ 属性：
    + `self.board`：棋盘
    + `self.current_player`：定义当前的下棋一方，考虑游戏还未开始我们定义为 None
    + `self.black_player`：定义黑棋玩家 black_player
    + `self.white_player`：定义白棋玩家 white_player

    
+ 方法：   
    + `switch_player()`：下棋时切换玩家  
    + `run()`：黑白棋游戏的主程序  


# 设计思想

## 蒙特卡洛方法(Monte Carlo method)
MCTS是一种“统计模拟方法”。20世纪40年代，为建造核武器，冯.诺伊曼等人发明了该算法。因赌城蒙特卡洛而得名，暗示其以概率作为算法的基础。
假设我们要计算一个不规则形状的面积，我们只需在包含这个不规则形状的矩形内，随机的掷出一个点，每掷出一个点，则N+1，如果这个点在不规则图形内则W+1。落入不规则图形的概率即为 W/N。当掷出足够多的点之后，我们可以认为：不规则图形面积＝矩形面积＊W/N。

## UCT（信心上限树算法）
UCT 算法是蒙特卡洛方法的一种改进，比蒙特卡洛方法更容易得 到最优解，其基本结构和蒙特卡洛方法相同，主要分为四个步骤：选 择 (Selection) ， 拓 展 (Expansion) ， 模 拟 (Simulation) 和 反 向 传 播 (Backpropagation)

**其价值函数定义为**
$$
value = child.reward / child.visits + c\sqrt{\frac{2In(node.visits)}{child.visits}}
$$

![image](https://pic4.zhimg.com/80/v2-16cafcfda07f07733d2a2326500b6bd7_720w.jpg)

### 选择(Selection)
在选择阶段，需要从根节点，也就是要做决策的局面R出发向下选择出一个最急迫需要被拓展的节点N，局面R是是每一次迭代中第一个被检查的节点；对于被检查的局面而言，他可能有三种可能：

+ 该节点所有可行动作都已经被拓展过
+ 该节点有可行动作还未被拓展过
+ 这个节点游戏已经结束了(例如已经连成五子的五子棋局面)
 

对于这三种可能：


+ 如果所有可行动作都已经被拓展过了，那么我们将使用UCB公式计算该节点所有子节点的UCB值，并找到值最大的一个子节点继续检查。反复向下迭代。
+ 如果被检查的局面依然存在没有被拓展的子节点(例如说某节点有20个可行动作，但是在搜索树中才创建了19个子节点)，那么我们认为这个节点就是本次迭代的的目标节点N，并找出N还未被拓展的动作A。执行步骤[2]
+ 如果被检查到的节点是一个游戏已经结束的节点。那么从该节点直接执行步骤{4]。
每一个被检查的节点的被访问次数在这个阶段都会自增。在反复的迭代之后，我们将在搜索树的底端找到一个节点，来继续后面的步骤。

### 拓展(Expansion)
在选择阶段结束时候，我们查找到了一个最迫切被拓展的节点N，以及他一个尚未拓展的动作A。在搜索树中创建一个新的节点Nn作为N的一个新子节点。Nn的局面就是节点N在执行了动作A之后的局面。

### 模拟(Simulation)
为了让Nn得到一个初始的评分。我们从Nn开始，让游戏随机进行，直到得到一个游戏结局，这个结局将作为Nn的初始评分。一般使用胜利/失败来作为评分，只有1或者0。

### 反向传播(Back Propagation)
在Nn的模拟结束之后，它的父节点N以及从根节点到N的路径上的所有节点都会根据本次模拟的结果来添加自己的累计评分。如果在[1]的选择中直接发现了一个游戏结局的话，根据该结局来更新评分。每一次迭代都会拓展搜索树，随着迭代次数的增加，搜索树的规模也不断增加。当到了一定的迭代次数或者时间之后结束，选择根节点下最好的子节点作为本次决策的结果。

## MCT伪代码

![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed/img/20210510192520.png)


# 代码内容

## 节点类的定义
    class Node:
        def __init__(self, state, parent=None, action=None, color="X"):
            self.visits = 0  #访问次数
            self.reward = 0.0 #期望值
            self.state = state #棋盘状态，Broad类
            self.children = [] #子节点
            self.parent = parent #父节点
            self.action = action #从父节点转移到本节点采取的动作
            self.color = color #该节点玩家颜色
    
        # 增加子节点
        def add_child(self, child_state, action, color):
            child_node = Node(child_state, parent=self, action=action, color=color)
            self.children.append(child_node)
    
        # 判断是否完全展开
        def fully_expanded(self):
            action = list(self.state.get_legal_actions(self.color))
            if len(self.children) == len(action):
                return True
            return False


## AI玩家类的定义

    class AIPlayer:
        """
        AI 玩家
        """
        step = 0
        def __init__(self, color):
            """
            玩家初始化
            :param color: 下棋方，'X' - 黑棋，'O' - 白棋
            """
            # 最大迭代次数
            self.max_times = 100
            # 玩家颜色
            self.color = color
            # UCB超参数
            self.SCALAR = 1
            
            
### 移动棋子的方法

    def get_move(self, board):
        """
        根据当前棋盘状态获取最佳落子位置
        :param board: 棋盘
        :return: action 最佳落子位置, e.g. 'A1'
        """
        if self.color == 'X':
            player_name = '黑棋'
        else:
            player_name = '白棋'
        print("请等一会，对方 {}-{} 正在思考中...".format(player_name, self.color))

        board_state = copy.deepcopy(board)
        root = Node(state=board_state, color=self.color)
        action = self.uct_search(self.max_times, root)

        return action

### UCT search的核心框架
    
    def uct_search(self, max_times, root):
        """
        根据当前棋盘状态获取最佳落子位置
        :param max_times: 最大搜索次数，默认100
        :param root: 根节点
        :return: action 最佳落子位置, e.g. 'A1'
        """
        for t in range(max_times):
            # print(t)
            leave = self.select_policy(root)
            reward = self.stimulate_policy(leave)
            self.backup(leave, reward)
            best_child = self.ucb(root, 0)
        return best_child.action
  
### 选择扩展的节点  
在这里对UCT的算法进行了改进，鼓励优先考虑目前期望值较大的节点，有0.5的概率在当前节点存在可扩展节点时选择不扩展

    def select_policy(self, node):
        """
        选择扩展的节点
        :param node: 根节点，Node 类
        :return: leave，Node 类
        """
        while not self.terminal(node.state):
            #node.state.display()
            #print(list(node.state.get_legal_actions(node.color)))
            if len(node.children) == 0:
                new_node = self.expand(node)
                #print(new_node.action)
                return new_node
            elif random.uniform(0, 1) < .5:
                node = self.ucb(node, self.SCALAR)
            else:
                node = self.ucb(node, self.SCALAR)
                if not node.fully_expanded():
                    return self.expand(node)
                else:
                    node = self.ucb(node, self.SCALAR)
        return node
        
### 扩展函数

    def expand(self, node):
        """
        选择扩展的节点
        :param node: 根节点，Node 类
        :return: leave，Node 类
        """
        # 随机选择动作
        action_list = list(node.state.get_legal_actions(node.color))
        # 防止尾盘时出现卡死，没有动作可以选择
        if len(action_list) == 0:
            return node.parent
        
        action = random.choice(action_list)
        tried_action = [c.action for c in node.children]
        while action in tried_action:
            action = random.choice(action_list)

        # 复制状态并根据动作更新到新状态
        new_state = copy.deepcopy(node.state)
        new_state._move(action, node.color)

        # 确定子节点颜色
        if node.color == 'X':
            new_color = 'O'
        else:
            new_color = 'X'

        # 新建节点
        node.add_child(new_state, action=action, color=new_color)
        return node.children[-1]

### ucb选择函数

    def ucb(self, node, scalar):
        """
        选择最佳子节点
        :param node: 节点，Node 类
        :param scalar: UCT公式超参数
        :return: best_child:最佳子节点，Node 类
        """
        best_score = -float('inf')
        best_children = []
        for c in node.children:
            exploit = c.reward / c.visits
            if c.visits == 0:
                best_children = [c]
                break
            explore = math.sqrt(2.0 * math.log(node.visits) / float(c.visits))
            score = exploit + scalar * explore
            if score == best_score:
                best_children.append(c)
            if score > best_score:
                best_children = [c]
                best_score = score
        if len(best_children) == 0:
            return node.parent
        return random.choice(best_children)
   
   ### 随机模拟对弈
在定义期望值时同时考虑了胜负关系和获胜的子数，board.get_winner()会返回胜负关系和获胜子数
在这里我们定义获胜积100分，每多赢一个棋子多1分
$$ 
reward = 100 + difference
$$


    def stimulate_policy(self, node):
        """
        随机模拟对弈
        :param node: 节点，Node 类
        :return: reward:期望值
        在定义期望值时同时考虑了胜负关系和获胜的子数，board.get_winner()会返回胜负关系和获胜子数
        在这里我们定义获胜积100分，每多赢一个棋子多1分
        reward = 100 + difference
        """
        board = copy.deepcopy(node.state)
        color = node.color
        count = 0
        while not self.terminal(board):
            action_list = list(node.state.get_legal_actions(color))
            if not len(action_list) == 0:
                action = random.choice(action_list)
                board._move(action, color)
                if color == 'X':
                    color = 'O'
                else:
                    color = 'X'
            else:
                if color == 'X':
                    color = 'O'
                else:
                    color = 'X'
                action_list = list(node.state.get_legal_actions(color))
                action = random.choice(action_list)
                board._move(action, color)
                if color == 'X':
                    color = 'O'
                else:
                    color = 'X'
            count = count + 1
            if count >= 10:
                break

        # 价值函数定义
        winner, difference = board.get_winner()
        if winner == 2:
            reward = 0
        elif winner == 1:
            reward = 100 + difference
        else:
            reward = -(100 + difference)

        if self.color == 'X':
            reward = - reward
        return reward
   
### 反向传播 
    def backup(self, node, reward):
        while node is not None:
            node.visits += 1
            if node.parent.color == self.color:
                node.reward += reward
            else:
                node.reward -= reward
            node = node.parent
        return 0

### 判断游戏是否结束
    def terminal(self, state):
        """
        判断游戏是否结束
        :return: True/False 游戏结束/游戏没有结束
        """

        # 根据当前棋盘，判断棋局是否终止
        # 如果当前选手没有合法下棋的位子，则切换选手；如果另外一个选手也没有合法的下棋位置，则比赛停止。
        b_list = list(state.get_legal_actions('X'))
        w_list = list(state.get_legal_actions('O'))

        is_over = len(b_list) == 0 and len(w_list) == 0  # 返回值 True/False

        return is_over
    
    



# 实验结果
## 初级
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed/img/20210510215115.png)

## 中级
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed/img/20210510215143.png)

## 高级
![](https://cdn.jsdelivr.net/gh/Fazziekey/image-bed/img/20210510215134.png)

在实际实验过程中基本可以碾压对手




[项目地址](https://github.com/Fazziekey/AI_project/tree/main/black-white-cheese)