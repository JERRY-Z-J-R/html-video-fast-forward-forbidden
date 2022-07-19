# HTML `<video>` 禁止 跳跃/拖动 ”播放条“的 JS 解决方案

> 很多业务场景下，我们需要让 `<video>` 中的视频不能进行快进（包括：跳跃、拖动），尤其是对于在线教育类视频课业务中，在学生没有看完全部时长的视频之前，需要设置为不允许跳跃或拖动播放条（视频条）快进，这里提供一个在原生的 `<video>` 标签下，利用 JavaScript 禁止 跳跃/拖动 ”播放条“的解决方案。

![demo](mark-img/demo.gif)

```html
<!DOCTYPE html>
<html lang="zh-CN">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HTML Video 禁止跳跃/拖动“播放条”快进</title>
</head>

<body>
    <div style="margin: 24px auto; width: 54%;">
        <video id="video" controls width="100%">
            <source src="video.mp4" type="video/mp4">
        </video>
    </div>

    <script>
        var video = document.getElementById("video");
        // 当前视频已播放到达过的最大时长
        var maxTime = 0;
        // seeked：当用户已经移动/跳跃到视频中新的位置时触发
        video.addEventListener('seeked', function () {
            // 移动/跳跃快进时，跳转回最大时长处
            if (this.currentTime > maxTime) {
                this.currentTime = maxTime;
            }
        }, false);
        // timeupdate：已播放时长改变时触发
        video.addEventListener('timeupdate', function () {
            if (this.currentTime - maxTime > 0 && this.currentTime - maxTime < 0.3) {
                // 更新最大时长
                maxTime = this.currentTime;
            }
        }, false);
    </script>
</body>

</html>
```

