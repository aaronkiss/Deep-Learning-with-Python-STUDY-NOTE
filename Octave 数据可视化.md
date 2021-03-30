## Octave 数据可视化
```octave

t = [0:0.01:0.98];    %生成一个向量。
y1 = sin(2*pi*4*t);    %定义y1函数。
plot(t,y1)    %绘制y1函数图像。
y2 = cos(2*pi*4*t);    %定义y2函数。
plot(t,y2)    %绘制y2函数图像。

%如果要将两个函数图像同时绘制出来：
plot(t,y1)    %先绘制y1图像。
hold on;    %用此命令保留已经绘制的图像。
plot(t,y2,'r')    %用红色绘制y2图像。

xlabel('time')    %给x轴标记为time标签。
ylabel('value')    %给y轴标记为value标签。

legend('sin','cos')    %标示图像的图例。
title('My plot')    %设定图像的标题。

print -dpng 'myPlot.png'    %将图像保存为指定名称与格式的图片文件。

close    %可以关闭已经生成的图像。

figure(1); plot(t,y1)    %将指定图像标注为指定名称。
figure(2); plot(t,y2)

subplot(1,2,1)    %将图像分为1*2的格子，然后使用第1个格子。

axis([0.5 1 -1 1])    %将坐标轴刻度缩放到指定范围。

clf    %清除图像。

A = magic(5)    %生成一个5*5的魔术方阵。

A =

    17    24     1     8    15
    23     5     7    14    16
     4     6    13    20    22
    10    12    19    21     3
    11    18    25     2     9

imagesc(A)    %绘制矩阵图形，颜色根据每个元素的值而不同。
imagesc(A), colorbar, colormap gray
%绘制图形，并生成刻度色带，并转换成灰度图。


```
