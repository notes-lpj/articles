#### 下载 m3u8 视频

```sh
ffmpeg -i 视频链接　本地存储文件名称 # https://ffmpeg.org/ffmpeg.html
```

- 视频链接获取方式：使用 chrome 播放视频，打开 console，按照下图的操作获取链接

![408da079-ca23-4d91-909d-ee588063d426](https://aliyun-oss-lpj.oss-cn-qingdao.aliyuncs.com/images/mass/408da079-ca23-4d91-909d-ee588063d426.png)

#### 剪切视频片段

```sh
ffmpeg -ss [start] -t [duration] -accurate_seek -i [in].mp4 -codec copy [out].mp4

[start]			# 为需要截取内容的开始时间
[duration]	# 为需要截取的时长
[in]				# 为输入视频文件名
[out]				# 为输出视频文件名
-to					#  截止到指定位置
```

#### 去除视频中的音频

```sh
ffmpeg -i input.mp4 -map 0:0 -vcodec copy out.mp4

# 注：
-map 		# 表示使用哪个流做为输入，0:0 表示第1个文件的每1个流
-vcodec # 表示使用流的视频，-acodec 表示使用流的音频，去除该参数，表示不需要音频
copy		# 表示要把新的流复制到新文件
```

#### flv to mp4

```sh
ffmpeg -i input.flv -codec copy output.mp4
```
