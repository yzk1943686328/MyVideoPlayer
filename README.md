Android视频播放器设计文档
最近学习了视频解码的有关内容，所以想要做一个视频播放器，Android中有专门用来处理多媒体的Mediaplayer，但使用起来不是很方便，很多东西都需要自己添加，所以我们这里使用Android中另一个原生组件-VideoView,VideoView是包装之后的MediaPlayer,可以和MediaController结合起来使用，自带开始，暂停，快进快退功能，而且还能拖动进度条，使用起来比较方便，所以我们使用VideoView+MediaController实现播放视频的功能。
首先我们需要简单的在界面中加入VideoView:
<VideoView
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:id="@+id/videoview">
</VideoView>
然后，我们就可以在MainActivity中使用VideoView了，我们需要设置设置VideoView的视频路径：
String videopath = "android.resource://" + getPackageName() + "/" + R.raw.yudie;
videoview.setVideoPath(videopath);
在这里我是把视频放在了res下的raw文件夹下，可以用"android.resource://" + getPackageName() + "/" + R.raw.yudie来获取mp4文件的路径，然后调用setVideoPath()方法设置VideoView的视频路径。
接下来，我们需要设置MediaController,使用方法很简单，new一个MediaController然后调用setMediaController()方法就可以了：
MediaController mediacontroller = new MediaController(this);
videoview.setMediaController(mediacontroller);
这样我们就可以实现播放视频的功能了，在Android手机上的截图如下：
                  
点击中间的符号可以控制播放或者暂停，左边的符号点一下可以快退15秒，右边的符号点击可以快进15秒，下方还有进度条，可以直接拖动。
其实视频播放器逼近可以用VideoView+MediaController实现，还可以用一种更原始的方法实现，MediaPlayer+SurfaceView结合也可以实现，关于这种方法，https://blog.csdn.net/liuzhi0724/article/details/81318816这个csdn博客写的比较详细，这里就不介绍了。
