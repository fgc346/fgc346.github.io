---
layout: post
title: 由矩形中心点求四个角点坐标
date: 2023-07-05
author: ego
tags: [数学]
categories: [数学]
toc: true
pinned: false
---


背景：

已知矩形的中心点坐标，知道矩形的长和宽，还有朝向，求四个角点的坐标。

## 代码

下面是python版本的代码：

```python
import matplotlib.pyplot as plt
from matplotlib.patches import Rectangle
import math

def draw_rectangle(center, orientation, length, width):
    # 创建一个图形对象
    fig, ax = plt.subplots()

    # 计算矩形的四个角点坐标
    angle = math.degrees(orientation)  # 将朝向转换为角度
    angle_rad = math.radians(angle)  # 将角度转换为弧度
    half_length = length / 2
    half_width = width / 2
    x = center[0]
    y = center[1]
   
    # 绘制四个角点坐标
    cos_angle = math.cos(angle_rad)
    sin_angle = math.sin(angle_rad)
    
    #左下角坐标
    left_rear_x = -half_length * cos_angle + half_width * sin_angle + x
    left_rear_y = -half_width * cos_angle - half_length * sin_angle + y
    print(f"left_rear_x:{left_rear_x}, left_rear_y:{left_rear_y}")
    
    #左上角坐标
    left_front_x =  -half_length * cos_angle - half_width * sin_angle + x
    left_front_y = half_width * cos_angle - half_length * sin_angle + y
    print(f"left_front_x:{left_front_x}, left_front_y:{left_front_y}")
    
    
    # 右上角坐标
    right_front_x = half_length * cos_angle - half_width * sin_angle + x
    right_front_y = half_width * cos_angle + half_length * sin_angle + y
    print(f"right_front_x:{right_front_x}, right_front_y:{right_front_y}")
    
    
    # 右下角坐标
    right_rear_x = half_length * cos_angle + half_width * sin_angle + x
    right_rear_y = half_length * cos_angle -half_width * sin_angle + y
    print(f"right_rear_x:{right_rear_x}, right_rear_y:{right_rear_y}")
    
    
    corners_2 = [
        (x + half_length * math.cos(angle_rad) - half_width * math.sin(angle_rad),
         y + half_length * math.sin(angle_rad) + half_width * math.cos(angle_rad)),
        (x + half_length * math.cos(angle_rad) + half_width * math.sin(angle_rad),
         y + half_length * math.sin(angle_rad) - half_width * math.cos(angle_rad)),
        (x - half_length * math.cos(angle_rad) + half_width * math.sin(angle_rad),
         y - half_length * math.sin(angle_rad) - half_width * math.cos(angle_rad)),
        (x - half_length * math.cos(angle_rad) - half_width * math.sin(angle_rad),
         y - half_length * math.sin(angle_rad) + half_width * math.cos(angle_rad))
    ]
    
    corners = [
        (left_rear_x, left_rear_y), 
        (left_front_x,left_front_y),
        (right_front_x, right_front_y),
        (right_rear_x, right_rear_y)
    ]

    # 创建矩形对象并添加到图形中
    rectangle = Rectangle((left_rear_x, left_rear_y), length, width, angle=angle, fill=False)
    ax.add_patch(rectangle)

    # 绘制矩形的四个角点
    for corner in corners:
        plt.plot(corner[0], corner[1], 'ro')
        
    # 绘制坐标原点
    plt.plot(center[0], center[1], 'b*')

    # 设置坐标轴范围
    ax.set_xlim([x - half_length - 1, x + half_length + 1])
    ax.set_ylim([y - half_width - 1, y + half_width + 1])

    # 显示图形
    plt.axis('equal')
    plt.show()

# 测试代码
if __name__ == "__main__":
    center = (1, 0)  # 中心点坐标
    orientation = math.radians(45)  # 朝向（以弧度表示）
    length = 4  # 长
    width = 2  # 宽
    draw_rectangle(center, orientation, length, width)


```

    left_rear_x:0.2928932188134523, left_rear_y:-2.1213203435596424
    left_front_x:-1.1213203435596428, left_front_y:-0.7071067811865474
    right_front_x:1.7071067811865477, right_front_y:2.1213203435596424
    right_rear_x:3.121320343559643, right_rear_y:0.7071067811865477

## 结果


![png](https://raw.githubusercontent.com/fgc346/image/main/img/output_0_1.png)
    



