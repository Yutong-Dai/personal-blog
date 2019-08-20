---
title: 中国传统计时
author: yutong
date: '2019-07-05'
slug: chinese-time
categories:
  - visualization
tags: [visualization]
subtitle: ''
summary: ''
authors: []
lastmod: '2019-07-05T15:58:50+08:00'
featured: yes
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---

# 中国传统计时单位

古时一天分12个时辰，采用地支作为时辰名称，分为

```
'子', '丑', '寅', '卯'
'辰', '巳', '午', '未' 
'申', '酉', '戌', '亥'
```
时辰的起点是午夜，即子初。

点击下图色块便可查看时间对应。
<iframe
      src="https://plot.ly/~Roth/2.embed"
      width="100%"
      height="600px"
      style="border:none;">
</iframe>


**附录**

1. 参考文献: 
  * [国学网](http://www.guoxue.com/?p=4025)
  * [新浪博客 博主知书少年果麦麦](https://weibo.com/6421571119/HBrUbvUnQ?from=page_1005056421571119_profile&wvr=6&mod=weibotime&type=comment#_rnd1562428488868)
2. 用于绘图的Python代码

```python
# using following code in jupyter notebook
import plotly
import plotly.graph_objs as go

plotly.offline.init_notebook_mode(connected=True)
colorPlate1 = [
    '#ffb3a7', 
    '#ffc773', '#ffa400',
    '#c9dd22', '#afdd22',
    '#cca4e3', '#b0a4e3',
    '#ffc64b', '#ffb61e',
    '#758a99', '#6b6882',
    '#ffb3a7', '#f47983',
    '#ffc773', '#ffa400',
    '#c9dd22', '#afdd22',
    '#cca4e3', '#b0a4e3',
    '#ffc64b', '#ffb61e',
    '#758a99', '#6b6882',
    '#f47983'
]
colorPlate2 = ['#ff4e20', '#ff7500', '#789262', '#8d4bbb', '#e9bb1d','#50616d'] * 2
theta_marker = ["{}:00".format(i) for i in range(24)]
timeStamp = [
'子正', '丑初', '丑正', '寅初', '寅正', 
'卯初', '卯正', '辰初', '辰正', '巳初', '巳正',  
'午初', '午正', '未初', '未正', '申初', '申正',  
'酉初', '酉正', '戌初', '戌正', '亥初', '亥正', '子初'
]
timeStampMain = [
'子, 名曰「困敦」<br>混沌万物之初萌，藏黄泉之下。<br> 子是兹的意思，这时候万物刚刚开始滋生和繁殖。', 
'丑, 名曰「赤奋若」<br>气运奋迅而起，万物无不若其性。<br>形容万物继续萌发，系于生长。', 
'寅, 名曰「摄提格」<br>万物承阳而起。<br>植物芽刚刚吐露，要吸收阳气生长，然后全部露出地面。',  
'卯, 名曰「单阏」<br>阳气推万物而起. <br>卯，就是茂，茂盛的样子。这个时候，万物生长滋生繁茂。', 
'辰, 名曰「执徐」<br>伏蛰之物，而敷舒出。<br>万物都震动而生长，草木伸舒，萌芽而出。', 
'巳, 名曰「大荒落<br>万物炽盛而出，霍然落之。<br>万物到了这个时候，都全部长起来了，聚集在一起。炽盛而有光泽的样子。',  
'午, 名曰「敦牂」<br>万物壮盛也。<br>万物都达到盛大壮茂，枝柯密布的状态。',
'未, 名曰「协洽」<br>阴阳和合，万物化生。<br>未，就是味的意思。当事物成熟的时候，都会发出气味。这时候阴气开始升起，万物稍微衰败。' ,
'申, 名曰「涒滩」<br>万物吐秀，倾垂也。<br>万物的身体都已成就，倾吐了最后的繁盛，引向衰败。',  
'酉, 名曰「作噩」<br>万物皆芒枝起。 <br>万物衰老到极至而成熟。',
'戌, 名曰「阉茂」<br>万物皆蔽冒也。<br>戌，灭，杀的意思。意思是到了这时候，万物都已经衰灭了。', 
'亥, 名曰「大渊献」<br>万物于天，深盖藏也。<br>亥，核的意思。万物都进入核阂里，意味着阴气劾杀了万物，等待下一个初萌。'
]

def sectorChild(name, location, radius,  fillcolor='#ff4e20'):
    r = [0] * 24
    r[location % 24] = radius
    r[(location + 1) % 24] = radius
    obj = go.Scatterpolar(
      name = name,
      r = r,
      theta = theta_marker,
      fill = "toself",
      fillcolor = fillcolor,
      line =  {"color":'black'}
    )
    return obj

def sectorParent(name, location, radius,  fillcolor='black'):
    r = [0] * 24
    if location == 0:
        r[0] = r[1] = r[23] = radius
    else:
        r[location % 24] = radius
        r[(location + 1) % 24] = radius
        r[(location + 2) % 24] = radius
    obj = go.Scatterpolar(
      name = name,
      r = r,
      theta = theta_marker,
      fill = "toself",
      fillcolor = fillcolor,
      line =  {"color":'black'},
      hoverinfo = 'text',
      hoverlabel = {'align':'left'}
    )
    return obj



trace = [sectorChild(i, j, 5, k) for (i,j,k) in zip(timeStamp, range(24), colorPlate1)]
trace += [sectorParent(timeStampMain[0], 0, 3, colorPlate2[0])]
trace += [sectorParent(i, j, 3, k) for (i,j, k) in zip(timeStampMain[1:], range(1, 23, 2), colorPlate2[1:]) ]

layout = go.Layout(
    polar = dict(
      radialaxis = dict(
        visible = False
      ),
      angularaxis = dict(
        direction = "clockwise",
        visible = True,
        linewidth = 3
      )
    ),
    showlegend = False
)


plotly.offline.iplot({
    "data": trace,
    "layout": layout
})
```

