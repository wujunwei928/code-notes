官方网站： http://ffmpeg.org/

官方文档: https://ffmpeg.org/documentation.html
Command Line Tools Documentation  
Components Documentation  

ffmpeg, ffplay, ffprobe

linux二进制下载： https://www.johnvansickle.com/ffmpeg/

[FFmpeg 基本用法](http://blog.csdn.net/doublefi123/article/details/24325159)

[雷霄骅的专栏](http://blog.csdn.net/leixiaohua1020)

何俊林的公众号 DriodDeveloper : ffmpeg 相关知识讲的非常棒

[使用 FFmpeg 处理高质量 GIF 图片](http://www.techug.com/post/high-quality-gif-with-ffmpeg.html)
ffmpeg默认生成的gif图像比较挫， 这篇文章介绍了怎么用来生成高质量的gif

[ffmpeg 调整音视频播放速度](http://blog.csdn.net/matrix_laboratory/article/details/53158307)

[ffmpeg filter学习-编写自己的filter](http://www.cnblogs.com/ranson7zop/p/7728639.html)

[使用ffmpeg为视频添加字幕](http://blog.csdn.net/u013699869/article/details/48162417)

[ffmpeg提升音频/视频音量命令](https://www.5yun.org/9377.html)

[ffmpeg 滤镜及其效果](http://blog.csdn.net/dangxw_/article/details/49001413)


```bash
#!/bin/sh

start_time=$3
duration=$4

palette="/tmp/palette.png"

filters="fps=15,scale=640:-1:flags=lanczos"

ffmpeg -v warning -ss $start_time -t $duration -i $1 -vf "$filters,palettegen" -y $palette
ffmpeg -v warning -ss $start_time -t $duration -i $1 -i $palette -lavfi "$filters [x]; [x][1:v] paletteuse" -y $2
```
创建一个用来生成gif的脚本 create_gif.sh
运行 ./create_git.sh t_1.mp4 a_3.gif 25 10


```bash
截取视频缩略图
ffmpeg -i 1.mp4 -r 3 -ss 00:00:26 -t 00:00:07 %03d.png

截取视频
 ffmpeg  -i 火影忍者vip-001.cn.cn.rmvb -ss 00:16:04 -to 00:16:53 1.mp4

合并视频
创建文件filelist.txt,内容如下
file '3_1.mp4'
file '3_2.mp4'
ffmpeg -f concat -i filelist.txt -c copy 3.mp4

转换视频格式
ffmpeg -i 1.mp4 2.avi

查看视频信息
ffmpeg -i 1.mp4

截取视频, 从视频的第5分钟开始截取
ffmpeg -ss 00:05:00 -i 1.mp4 -c copy -t 360 4.mp4

从视频的第5分钟开发, 截取6秒钟的视频
ffmpeg -ss 00:05:00 -t 6 -i 1.mp4 -c copy -t 360 3.mp4


ffmpeg替换视频中的音频方法
步骤一：ffmpeg提取视频
ffmpeg -i test.mp4 -vcodec copy -an 视频流.avi
步骤二：ffmpeg替换音频命令（就是把音频视频合并起来）
ffmpeg -i 视频流.avi -i 音频流.mp3 -vcodec mpeg4 -acodec copy 合并.mp4

添加水印
ffmpeg -i test.mp4 -i logo.png -filter_complex overlay test1.mp4
在视频的右下角添加gif图片
ffmpeg -y -i test2.mp4 -ignore_loop 0 -i test.gif  -filter_complex overlay=0:H-h test_out2.mp4

setopts将时间缩短为原来的0.5, -r 码率设置为原来的0.5, 播放速度会是原来的二倍
ffmpeg -i 1.mp4 -r 12 -filter:v "setpts=0.5*PTS" 2.mp4

-s 设置分辨率
ffmpeg -i 1.mp4 -s 600x338 2.mp4

视频裁剪,  默认是从坐标(0,0)裁剪, 视频左上角为坐标原点
1: 从坐标(0,0)裁剪, 输出宽度=输入宽度, 输出高度=输入高度*0.8
ffmpeg -i 2.mp4 -filter:v "crop=out_w=in_w:out_h=0.8*in_h" 2.mp4
1: 从坐标(0,0.2*in_h)裁剪, 输出宽度=输入宽度, 输出高度=输入高度*0.8
fffmpeg -i 2.mp4 -ss 50 -t 10 -filter:v "crop=in_w:0.8*in_h:0:0.2*in_h" 3_caijian.mp4
```
