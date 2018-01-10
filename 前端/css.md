# css

## 由css的transform：rotate引发的一系列的问题
> 一些资料
有关于transform的matrix详见：张鑫旭css
http://www.zhangxinxu.com/wordpress/2012/06/css3-transform-matrix-%E7%9F%A9%E9%98%B5/
* transform:translate(x,y)  ---> transform: matrix(1,0,0,1,x,y);
* transform:scale(x,y) ---> transform:maxtrix(x,0,0,y,0,0);
* transform:rotate(θ) ---> matrix(cosθ,sinθ,-sinθ,cosθ,0,0);
* transform:skew(x + 'deg', y + 'deg') ---> matrix(1,tan(θy),tan(θx),1,0,0);

> sin(x + y) = sin(x)cos(y) + cos(x)sin(y)
> cos(x + y) = cos(x)cos(y) -sin(x)sin(y)
> http://math2.org/math/algebra/functions/sincos/properties.htm

* 对于做旋转动画的元素而言，通过`getComputedStyle(ele).transform`可以实时的计算出元素的旋转量，会发现其角度是一直在增加了，也可以认为是一直是0-2PI
* 对于一个做旋转动画的元素，如下代码所示，当动画设置`animation-play-state:paused`时动画停止，此时动画元素的旋转量为0；（即恢复到了初始状态）
* 在音乐播放器实例中，cd的旋转表明了歌曲播放状态，点击暂停时，为了保持cd的偏移状态，需要使用外部容器记录旋转状态，这就需要让外部容器的旋转角度加上内部图片的角度；这便涉及到以上所提到的问题。
```
    @keyframes rotate {
      0% {
        transform: rotate(0);
      }
      100% {
        // deg 角度单位 360deg
        // rad 弧度单位 3.1415926rad * 2
        transform: rotate(3.1415926rad * 2);
      }
    }
    animation-play-state: paused;
```


