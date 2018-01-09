# css 

## 有关于transform的matrix详见：张鑫旭css
http://www.zhangxinxu.com/wordpress/2012/06/css3-transform-matrix-%E7%9F%A9%E9%98%B5/
* transform:translate(x,y)  ---> transform: matrix(1,0,0,1,x,y);
* transform:scale(x,y) ---> transform:maxtrix(x,0,0,y,0,0);
* transform:rotate(θ) ---> matrix(cosθ,sinθ,-sinθ,cosθ,0,0);
* transform:skew(x + 'deg', y + 'deg') ---> matrix(1,tan(θy),tan(θx),1,0,0);
> sin(x + y) = sin(x)cos(y) + cos(x)sin(y)
> cos(x + y) = cos(x)cos(y) -sin(x)sin(y)
> http://math2.org/math/algebra/functions/sincos/properties.htm