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
      height="500px"
      style="border:none;">
</iframe>


**附录**

1. 参考文献: [国学网](http://www.guoxue.com/?p=4025)
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
'子', '丑', '寅', 
'卯', '辰', '巳',  
'午', '未', '申',  
'酉', '戌', '亥'
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
      line =  {"color":'black'}
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

