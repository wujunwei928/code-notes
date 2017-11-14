官方网站： http://ffmpeg.org/

linux二进制下载： https://www.johnvansickle.com/ffmpeg/

[FFmpeg 基本用法](http://blog.csdn.net/doublefi123/article/details/24325159)

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
```
