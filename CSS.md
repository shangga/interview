# CSS总结
## flex与传统布局的差异 
    传统的布局是基于css盒模型，依赖display＋position＋float等属性
    flex是弹性布局，为盒模型提供最大程度的灵活性
## transform
    所有的transform属性的参考位置都是元素中心点，可以通过transform-origin属性设置，默认值是50%，50%
    skew(): 相对于x轴，y轴的移动
    translate(): 从当前位置移动
    rotate(): 旋转角度
    scale(): 放大缩小
    matrix(): 所有的2D转换方法集合，包含数学函数，允许您：旋转、缩放、移动以及倾斜元素   

## 不定宽高元素的垂直水平居中
    transform：translate（－50%，－50%）；
    position：absolute；
    top：50%；
    left：50％；