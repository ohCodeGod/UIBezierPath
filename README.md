# UIBezierPath

   UIBezierPath对象是CGPathRef数据类型的封装。path如果是基于矢量形状的，都用直线和曲线段去创建。我们使用直线段去创建矩形和多边形，使用曲线段去创建弧（arc），圆或者其他复杂的曲线形状。每一段都包括一个或者多个点，绘图命令定义如何去诠释这些点。每一个直线段或者曲线段的结束的地方是下一个的开始的地方。每一个连接的直线或者曲线段的集合成为subpath。一个UIBezierPath对象定义一个完整的路径包括一个或者多个subpaths。

UIBezierPath类头文件定义
// 根据一个Rect画一个矩形曲线

+ (instancetype)bezierPath;



/**

 *  根据一个Rect画一个椭圆曲线  Rect为正方形时画的是一个圆

 *  @param rect CGRect一个矩形

 */

+ (instancetype)bezierPathWithRect:(CGRect)rect;



/**

 *  根据一个Rect画一个圆角矩形曲线 (Radius:圆角半径)   当Rect为正方形时且Radius等于边长一半时画的是一个圆

 *  @param rect CGRect一个矩形

 */

+ (instancetype)bezierPathWithOvalInRect:(CGRect)rect;



/**

 *  根据一个Rect画一个圆角矩形曲线   当Rect为正方形时且Radius等于边长一半时画的是一个圆

 *  @param rect         CGRect一个矩形

 *  @param cornerRadius 圆角半径

 */

+ (instancetype)bezierPathWithRoundedRect:(CGRect)rect cornerRadius:(CGFloat)cornerRadius;



typedef NS_OPTIONS(NSUInteger, UIRectCorner) {

    UIRectCornerTopLeft     = 1 << 0,

    UIRectCornerTopRight    = 1 << 1,

    UIRectCornerBottomLeft  = 1 << 2,

    UIRectCornerBottomRight = 1 << 3,

    UIRectCornerAllCorners  = ~0UL

};

/**

 *  根据一个Rect针对四角中的某个或多个角设置圆角

 *

 *  @param rect        CGRect一个矩形

 *  @param corners     允许指定矩形的部分角为圆角，而其余的角为直角，取值来自枚举 

 *  @param cornerRadii  指定了圆角的半径，这个参数的取值是 CGSize 类型，也就意味着这里需要给出的是椭圆的半径。

 */

+ (instancetype)bezierPathWithRoundedRect:(CGRect)rect byRoundingCorners:(UIRectCorner)corners cornerRadii:(CGSize)cornerRadii;



/**

 *  以某个中心点画弧线

 *  @param center     指定了圆弧所在正圆的圆心点坐标

 *  @param radius     指定了圆弧所在正圆的半径

 *  @param startAngle 指定了起始弧度位置  注意: 起始与结束这里是弧度 

 *  @param endAngle   指定了结束弧度位置  

 *  @param clockwise  指定了绘制方向，以时钟方向为判断基准   看下图

 */

+ (instancetype)bezierPathWithArcCenter:(CGPoint)center radius:(CGFloat)radius startAngle:(CGFloat)startAngle endAngle:(CGFloat)endAngle clockwise:(BOOL)clockwise;

图片来自网络



 

/**

 *  根据CGPath创建并返回一个新的UIBezierPath对象

 *  @param CGPath CGPathRef

 */

+ (instancetype)bezierPathWithCGPath:(CGPathRef)CGPath;

 



@property(nonatomic)CGPathRef CGPath;





- (CGPathRef)CGPathNS_RETURNS_INNER_POINTER CF_RETURNS_NOT_RETAINED;





/**

 *  设置第一个起始点到接收器

 *  @param point 起点坐标

 */

- (void)moveToPoint:(CGPoint)point;



/**

 *  附加一条直线到接收器的路径

 *  @param point 要到达的坐标

 */

- (void)addLineToPoint:(CGPoint)point;



/**

 *  该方法就是画三次贝塞尔曲线的关键方法，以三个点画一段曲线，一般和moveToPoint:配合使用。其实端点为moveToPoint:设置，终止端点位为endPoint；。控制点1的坐标controlPoint1，这个参数可以调整。控制点2的坐标是controlPoint2。

 *

 *  @param endPoint      终点坐标

 *  @param controlPoint1 控制点1

 *  @param controlPoint2 控制点2  看下图

 */

- (void)addCurveToPoint:(CGPoint)endPoint controlPoint1:(CGPoint)controlPoint1 controlPoint2:(CGPoint)controlPoint2;

图片来自网络





/**

 *  画二次贝塞尔曲线，是通过调用此方法来实现的。一般和moveToPoint:配合使用。endPoint终端点，controlPoint控制点，对于二次贝塞尔曲线，只有一个控制点

 *  @param endPoint     终点坐标

 *  @param controlPoint 控制点  看下图

 */

- (void)addQuadCurveToPoint:(CGPoint)endPoint controlPoint:(CGPoint)controlPoint;

图片来自网络





/**

 *  添加一个弧线 与bezierPathWithArcCenter:radius:startAngle:endAngle:clockwise:区别是bezierPathWithArcCenter它是初始化一个弧线,addArcWithCenter是添加一个弧线,共同点就是参数都一样

 *  @param center     指定了圆弧所在正圆的圆心点坐标

 *  @param radius     指定了圆弧所在正圆的半径

 *  @param startAngle 指定了起始弧度位置

 *  @param endAngle   指定了结束弧度位置

 *  @param clockwise  指定了绘制方向，以时钟方向为判断基准

 */

- (void)addArcWithCenter:(CGPoint)center radius:(CGFloat)radius startAngle:(CGFloat)startAngle endAngle:(CGFloat)endAngle clockwise:(BOOL)clockwise NS_AVAILABLE_IOS(4_0);



/**

 *  闭合线使用这个方法起始点与终点将相连

 */

- (void)closePath;



/**

 *  移除所有坐标点

 */

- (void)removeAllPoints;



// Appending paths

// 添加一个paths UIBezierPath

- (void)appendPath:(UIBezierPath *)bezierPath;



// Modified paths

// 创建并返回一个与当前路径相反的新的贝塞尔路径对象

- (UIBezierPath *)bezierPathByReversingPath NS_AVAILABLE_IOS(6_0);



// Transforming paths

// 用指定的仿射变换矩阵变换路径的所有点

- (void)applyTransform:(CGAffineTransform)transform;



// Path info

// 该值指示路径是否有任何有效的元素。

@property(readonly,getter=isEmpty)BOOL empty;

// 路径包括的矩形

@property(nonatomic,readonly)CGRect bounds;

// 图形路径中的当前点

@property(nonatomic,readonly)CGPoint currentPoint;

// 接收器是否包含指定的点

- (BOOL)containsPoint:(CGPoint)point;



// Drawing properties

// 线宽

@property(nonatomic)CGFloat lineWidth;



typedef CF_ENUM(int32_t, CGLineCap) {

    kCGLineCapButt,  默认的

    kCGLineCapRound, 轻微圆角

    kCGLineCapSquare 正方形

};

// 端点类型

@property(nonatomic)CGLineCap lineCapStyle;


typedef CF_ENUM(int32_t, CGLineJoin) {

    kCGLineJoinMiter, 默认的表示斜接

    kCGLineJoinRound, 圆滑衔接

    kCGLineJoinBevel  斜角连接

};

// 连接类型

@property(nonatomic)CGLineJoin lineJoinStyle;



// 最大斜接长度   斜接长度指的是在两条线交汇处内角和外角之间的距离

@property(nonatomic)CGFloat miterLimit;// Used when lineJoinStyle is kCGLineJoinMiter



/* 

 最大斜接长度   斜接长度指的是在两条线交汇处内角和外角之间的距离

 只有lineJoin属性为kCALineJoinMiter时miterLimit才有效

 边角的角度越小，斜接长度就会越大。

 为了避免斜接长度过长，我们可以使用 miterLimit属性。

 如果斜接长度超过 miterLimit的值，边角会以 lineJoin的 "bevel"即kCALineJoinBevel类型来显示

*/





// 确定弯曲路径短的绘制精度的因素

@property(nonatomic)CGFloat flatness;

// 一个bool值指定even-odd规则是否在path可用

@property(nonatomic)BOOL usesEvenOddFillRule;// Default is NO. When YES, the even-odd fill rule is used for drawing, clipping, and hit testing.

// 设置线型 可设置成虚线

CGFloat pattern[] = {1,1};

- (void)setLineDash:(nullableconst CGFloat *)pattern count:(NSInteger)count phase:(CGFloat)phase;

//  检索线型

- (void)getLineDash:(nullableCGFloat *)pattern count:(nullableNSInteger *)count phase:(nullableCGFloat *)phase;



// Path operations on the current graphics context 当前图形上下文中的路径操作：

// 填充颜色

- (void)fill;



// 利用当前绘图属性沿着接收器的路径绘制

- (void)stroke;



// These methods do not affect the blend mode or alpha of the current graphics context

// 用指定的混合模式和透明度值来描绘受接收路径所包围的区域

- (void)fillWithBlendMode:(CGBlendMode)blendMode alpha:(CGFloat)alpha;



// 使用指定的混合模式和透明度值沿着接收器路径。绘制一行

- (void)strokeWithBlendMode:(CGBlendMode)blendMode alpha:(CGFloat)alpha;



// 剪切被接收者路径包围的区域该路径是带有剪切路径的当前绘图上下文。使得其成为我们当前的剪切路径

- (void)addClip;



实践~敲出如下图代码


- (void)drawRect:(CGRect)rect {



    UIColor *brushColor = [UIColorwhiteColor];

    

    // 根据一个Rect 画一个矩形曲线

    UIBezierPath *rectangular = [UIBezierPathbezierPathWithRect:CGRectMake(5,5, 30, 30)];

    [PNRed set];

    [rectangular fill];

    [brushColor set];

    [rectangular stroke];

    

    // 根据一个Rect画一个椭圆曲线  Rect为正方形时画的是一个圆

    UIBezierPath *oval = [UIBezierPathbezierPathWithOvalInRect:CGRectMake(40,5, 50,30)];

    [PNBlue set];

    [oval fill];

    [brushColor set];

    [oval stroke];

    

    // 根据一个Rect 画一个圆角矩形曲线 (Radius:圆角半径)   当Rect为正方形时且Radius等于边长一半时画的是一个圆

    UIBezierPath *roundedRect = [UIBezierPathbezierPathWithRoundedRect:CGRectMake(95,5, 40,30) cornerRadius:5];

    [PNStarYellow set];

    [roundedRect fill];

    [brushColor set];

    [roundedRect stroke];

    

    // 根据一个Rect针对四角中的某个或多个角设置圆角

    UIBezierPath *roundedRect2 = [UIBezierPathbezierPathWithRoundedRect:CGRectMake(140,5, 40,30) byRoundingCorners:UIRectCornerTopLeft|UIRectCornerBottomRightcornerRadii:CGSizeMake(10,50)];

    [PNFreshGreen set];

    [roundedRect2 fill];

    [brushColor set];

    [roundedRect2 stroke];



    // 以某个中心点画弧线

    UIBezierPath *arcPath = [UIBezierPathbezierPathWithArcCenter:CGPointMake(200,15) radius:20startAngle:0endAngle:degreesToRadian(90)clockwise:YES];

    [brushColor set];

    [arcPath stroke];

    

    // 添加一个弧线

    UIBezierPath *arcPath2 = [UIBezierPathbezierPath];

    [arcPath2 moveToPoint:CGPointMake(230,30)];

    [arcPath2 addArcWithCenter:CGPointMake(265,30) radius:25startAngle:degreesToRadian(180)endAngle:degreesToRadian(360)clockwise:YES];

    // 添加一个UIBezierPath

    [arcPath2 appendPath:[UIBezierPathbezierPathWithArcCenter:CGPointMake(265,30) radius:20startAngle:0endAngle:M_PI*2clockwise:YES]];

    [PNStarYellow set];

    [arcPath2 stroke];

    

    // 根据CGPath创建并返回一个新的UIBezierPath对象

    UIBezierPath *be = [selfbezierPathWithCGPath];

    [PNRed set];

    [be stroke];

    

    // 三角形

    UIBezierPath *triangle = [UIBezierPathbezierPath];

    [triangle moveToPoint:CGPointMake(145,165)];

    [triangle addLineToPoint:CGPointMake(155,185)];

    [triangle addLineToPoint:CGPointMake(135,185)];

    [PNStarYellow set];

    [triangle fill];

//    [triangle stroke];

    [triangle closePath];

    

    // 二次贝塞尔曲线

    UIBezierPath *quadBe = [UIBezierPathbezierPath];

    [quadBe moveToPoint:CGPointMake(30,150)];

    [quadBe addQuadCurveToPoint:CGPointMake(130,150) controlPoint:CGPointMake(30,70)];

    

    UIBezierPath *quadBe2 = [UIBezierPathbezierPath];

    [quadBe2 moveToPoint:CGPointMake(160,150)];

    [quadBe2 addQuadCurveToPoint:CGPointMake(260,150) controlPoint:CGPointMake(210,50)];

    [quadBe2 appendPath:quadBe];

    quadBe2.lineWidth = 1.5f;

    quadBe2.lineCapStyle = kCGLineCapSquare;

    quadBe2.lineJoinStyle = kCGLineJoinRound;

    [brushColor set];

    [quadBe2 stroke];

    

    // 三次贝塞尔曲线

    UIBezierPath *threePath = [UIBezierPathbezierPath];

    [threePath moveToPoint:CGPointMake(30,250)];

    [threePath addCurveToPoint:CGPointMake(260,230) controlPoint1:CGPointMake(120,180) controlPoint2:CGPointMake(150,260)];

    threePath.lineWidth = 1.5f;

    threePath.lineCapStyle = kCGLineCapSquare;

    threePath.lineJoinStyle = kCGLineJoinRound;

    [brushColor set];

    [threePath stroke];

}


- (UIBezierPath *)bezierPathWithCGPath {

    UIBezierPath *framePath;

    CGFloat arrowWidth = 14;

    

    CGMutablePathRef path =CGPathCreateMutable();

    

    CGRect rectangle =CGRectInset(CGRectMake(0,0, CGRectGetWidth(self.bounds),CGRectGetWidth(self.bounds)),3,3);

    

    CGPoint p[3] = {

        

    {CGRectGetMidX(self.bounds)-arrowWidth/2,CGRectGetWidth(self.bounds)-6},

        

    {CGRectGetMidX(self.bounds)+arrowWidth/2,CGRectGetWidth(self.bounds)-6},

        

    {CGRectGetMidX(self.bounds),CGRectGetHeight(self.bounds)-4}

        

    };

    

    CGPathAddRoundedRect(path, NULL, rectangle, 5, 5);

    

    CGPathAddLines(path, NULL, p, 3);

    

    CGPathCloseSubpath(path);

    // 根据CGPath创建并返回一个新的UIBezierPath对象

    framePath = [UIBezierPath bezierPathWithCGPath:path];

    

    CGPathRelease(path);

    

    return framePath;

}
