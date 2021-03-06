---
title:  "unity攻击范围检测的方式区别"
---

#### 1.利用碰撞器的触发器Trigger

  这种是比较基础的做法，利用OnTriggerEntry函数，当目标进入触发器时触发。例如玩家有一把剑，我要做攻击判定的话，我就可以在剑上挂一个触发器，设定好大小，当播放动画时，随着剑的挥动，目标会进入Trigger的范围，此时就会调用OnTriggerEntry函数。但是这样做有个弊端，如果挥舞速度太快，检测会有问题；还有就是必须满足“进入”这个条件，也就是说如果原来目标就在触发器范围内，或者触发器在目标内，是不会触发函数的。所以这种方法不太适用于3D游戏。

  不过这种方法也不是不能用，只是适用条件有限，在2D游戏上，结合上Animation的录制功能，通过动画来改变Trigger的大小，这样就可以触发OnTriggerEntry函数一次或者多次，这样也是可以做出不错效果的。在3D游戏中，可以在人物前面放置一个大小合适Trigger当做攻击范围，再结合动画事件进行攻击判定，不过这样做的缺点是攻击范围大小恒定，如果人物的攻击范围大小不一，就要创建很多空子物体来设定Trigger范围，脚本也不好管理。

#### 2.利用数学判断

  可以定义两个向量作为攻击范围，向量有方向也有长度，攻击范围是可以确定的。例如设定两个向量，向量1为Transform.forward的左偏45度，向量2为Transform.forward的右偏45度，长度均为5。此时攻击范围为半径为5，度数为90°的扇形。此时就可以计算敌人是不是在攻击范围内，可以通过Vector3.Angle来计算（角度制），Vector3.Distance来计算距离。

  这种方法的局限在于1.如何获取到敌人的游戏物体，可以通过触发器也可以遍历你的敌人列表。2.当敌人体积过大时，有可能身体的一部分已经进入攻击范围，但是postion没有进入攻击范围，此时判定就会出现错误。看情况使用。

#### 3.利用射线Raycast

  使用Physics.Raycast()这个方法来发射射线，当射线碰到物体，或者碰到指定Laymask层的物体，或者一定距离后就会返回，返回值是Bool类型。通过out关键字来输出碰撞到的物体的信息，变量类型为RaycastHit。例如我定义一个射线Ray ray =new Ray(), 一个射线返回RaycastHit hit，那么就应该这么使用Physics.Raycast(ray,out hit),表示碰到物体，就会返回ture，物体信息储存在hit中。没有碰到，就会范围false，hit为null。这个方法还有很多重载，可以自己查阅API，根据情况使用。

  这种方法是射击游戏的常用判断方法，可以结合lineRender来渲染子弹飞过的特效。不过这种方法也不是万能的，它的局限在于射出射线的点只有一个，用来做射击游戏的攻击判定是非常合适的，但是不能用来做判定比较严格的游戏。为什么呢，因为射击游戏的发射方向是可以根据准星调整的，视觉上的判定也是准星方向，如果是动作游戏，rpg游戏之类的，攻击类型多样，就会出现差错。例如一个从上至下的斩击，攻击范围应该是竖着的一条线，那么射线应该怎发射呢？如果直直的往前发射，那么当敌人蹲下的时候，就会检测不到。你或许会想做成动作模式不就完了吗？（就是类似于龙之谷的操作方式），也是不行的，判定始终在攻击轨迹中央，和攻击动画和攻击特效有出入。

#### 4.利用射线Linecast 

  这也是Physics的一个方法， Physics.Linecast（）。连接两个点形成线段，如果线段中间有物体，就返回true,否则返回flase，同样，这个方法需要定义一个RaycastHit类型的变量来接收返回数据，具体方法为Physics.Linecast（Vector3 point1, Vector3 point2，out hit）。这种方法需要在武器或者拳头或者其他的需要攻击判定的地方设定一个点，当动画播放时，这个点的世界坐标就会变化，此时我们可以选择记录某几个时间点上判定点的世界坐标，再用Linecast进行判定。一般取判定点的坐标的话我们同样可以利用动画事件。

  这种方法调试的时候最好用lineRender把攻击轨迹渲染出来，或者用Debug.DrawLine()画出来（记得设定存在时间，不然一瞬间就消失了看不到），这样可以方便调整我们取判定点的时间节点，不然可能会疑惑，明明我设定好了，怎么检测不到。这种方法适合于动作游戏，以及一些判定比较精细的游戏。需要注意的一点是，Linecast每一帧都会进行判定，一般我们只需要一个动作判定一次，那么还需要在代码里进行约束。



