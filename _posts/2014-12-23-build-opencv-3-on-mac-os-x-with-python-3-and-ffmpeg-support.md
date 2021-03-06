---
layout: post
title: Build OpenCV 3 on Mac OS X with Python 3 and ffmpeg support
author: Jia Shen Boon
tags:
blogger_id: tag:blogger.com,1999:blog-6651978490904982752.post-4389063515094275109
blogger_orig_url: http://blog.jiashen.me/2014/12/build-opencv-3-on-mac-os-x-with-python.html
---


Today I'll be talking about... exactly what the title suggests! I got an idea a couple of days back for a video processing project and I decided that I was going to use Python 3 and OpenCV 3, because I like shiny new things. I ran into a little bit of trouble getting ffmpeg support on OpenCV, and without it you can't grab frames from a video file. But with my Google-Fu and sheer genius I eventually pulled through.

Here's the instructions!

1. Install ffmpeg using Homebrew (terminal command: `brew install ffmpeg`)
2. Follow instructions on [Luis González's blog post](http://luigolas.com/blog/2014/09/15/install-opencv3-with-python-3-mac-osx/) EXCEPT when you're configuring the OpenCV build, also
- Set `FFMPEG_INCLUDE_DIR` as `/usr/local/Cellar/ffmpeg/2.4.2/include/`
- Set `FFMPEG_LIB_DIR` as `/usr/local/Cellar/ffmpeg/2.4.2/lib/`
(You can type `ffmpeg` in your terminal to find the exact paths for the two values above)
- Tick the box of `WITH_FFMPEG`
3. Continue with Luis González's instructions and you should be good!

To test whether the codec worked, you can try something like the following:

~~~
import cv2

cap = cv2.VideoCapture('my_video.mp4')

frames = []
while cap.isOpened():

    # Capture frame-by-frame
    read_success, frame = cap.read()

    if not read_success:
        break

    frames.append(frame)

print('Grabbed ', len(frames), ' frames')
~~~
{: .language-python}

Hope this was helpful!

<!--
<span id="docs-internal-guid-01fd1b72-7428-8c38-8e94-31e86468a974"></span><br /><div><span style="font-family: Arial;"><span style="font-size: 15px; line-height: 17.25px; white-space: pre-wrap;">Today I'll be talking about... exactly what the title suggests! I got an idea a couple of days back for a video processing project and I decided that I was going to use Python 3 and OpenCV 3, because I like shiny new things. I ran into a little bit of trouble getting ffmpeg support on OpenCV, and without it you can't grab frames from a video file. But with my Google-Fu and sheer genius I eventually pulled through.</span></span></div><div><span style="font-family: Arial;"><span style="font-size: 15px; line-height: 17.25px; white-space: pre-wrap;"><br /></span></span></div><div><span style="font-family: Arial;"><span style="font-size: 15px; line-height: 17.25px; white-space: pre-wrap;">Here's the instructions!</span></span></div><div><span style="font-family: Arial;"><span style="font-size: 15px; line-height: 17.25px; white-space: pre-wrap;"><br /></span></span></div><ol style="margin-bottom: 0pt; margin-top: 0pt;"><li dir="ltr" style="background-color: transparent; color: black; font-size: 15px; font-style: normal; font-variant: normal; font-weight: normal; list-style-type: decimal; text-decoration: none; vertical-align: baseline;"><div dir="ltr" style="line-height: 1.15; margin-bottom: 0pt; margin-top: 0pt;"><span style="font-family: Arial; line-height: 1.15; white-space: pre-wrap;">Install ffmpeg using Homebrew (terminal command: </span><span style="line-height: 1.15; white-space: pre-wrap;"><span style="font-family: Courier New, Courier, monospace;">brew install ffmpeg</span><span style="font-family: Arial;">)</span></span></div></li><li dir="ltr" style="background-color: transparent; color: black; font-size: 15px; font-style: normal; font-variant: normal; font-weight: normal; list-style-type: decimal; text-decoration: none; vertical-align: baseline;"><span style="font-family: Arial;"><span style="line-height: 1.15; white-space: pre-wrap;">Follow instructio</span></span>ns on&nbsp;<a href="http://luigolas.com/blog/2014/09/15/install-opencv3-with-python-3-mac-osx/">Luis González's blog post</a>&nbsp;<span style="font-family: Arial; line-height: 1.15; white-space: pre-wrap;"><b>EXCEPT</b> when you're configuring the OpenCV build, also</span></li><ul><li><span style="font-family: Arial; font-size: 15px; line-height: 1.15; white-space: pre-wrap;">Set <i>FFMPEG_INCLUDE_DIR</i> as <i>/usr/local/Cellar/ffmpeg/2.4.2/include/</i></span></li><li><span style="font-family: Arial; font-size: 15px; line-height: 1.15; white-space: pre-wrap;">Set <i>FFMPEG_LIB_DIR</i> as <i>/usr/local/Cellar/ffmpeg/2.4.2/lib/</i></span></li><li><span style="font-size: 15px; line-height: 17.25px; white-space: pre-wrap;"><span style="font-family: Arial;">(You can type </span><span style="font-family: Courier New, Courier, monospace;">ffmpeg</span><span style="font-family: Arial;"> in your terminal to find the exact paths for the two values above)</span></span></li><li><span style="font-family: Arial; font-size: 15px; line-height: 1.15; white-space: pre-wrap;">Tick the box of <i>WITH_FFMPEG</i></span></li></ul><li dir="ltr" style="background-color: transparent; color: black; font-family: Arial; font-size: 15px; font-style: normal; font-variant: normal; font-weight: normal; list-style-type: decimal; text-decoration: none; vertical-align: baseline;"><span style="background-color: transparent; color: black; font-family: Arial; font-size: 15px; font-style: normal; font-variant: normal; font-weight: normal; text-decoration: none; vertical-align: baseline; white-space: pre-wrap;">Continue with<span style="font-family: 'Times New Roman'; font-size: small; white-space: normal;">&nbsp;</span>Luis González's instructions and you should be good!</span></li></ol><div><span style="font-family: Arial;"><span style="font-size: 15px; white-space: pre-wrap;"><br /></span></span></div><div><span style="font-family: Arial;"><span style="font-size: 15px; white-space: pre-wrap;">To test whether the codec worked, you can try something like the following:</span></span></div><div><span style="font-family: Arial;"><span style="font-size: 15px; white-space: pre-wrap;"><br /></span></span></div><div><pre>    import cv2</pre><pre>   &nbsp;</pre><pre>    cap = cv2.VideoCapture('my_video.mp4')<br /><br />    frames = []<br />    while cap.isOpened():<br /><br />        # Capture frame-by-frame<br />        read_success, frame = cap.read()<br /><br />        if not read_success:<br />            break<br /><br />        frames.append(frame)</pre><pre><br /></pre><pre>    print('Grabbed ', len(frames), ' frames')</pre><pre><br /></pre><pre><span style="font-family: Arial; font-size: 15px; white-space: pre-wrap;">Hope this was helpful!</span></pre></div> -->