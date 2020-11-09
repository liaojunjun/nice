### 容器和项目

采用网格布局的区域，称为容器(container),子元素称为项目

### 行和列

row column

### 单元格

row \* column

### 网格线

grid line，n 行有 n + 1 根水平网格线，m 列有 m + 1 根垂直网格线

### 容器属性

- display: grid;设为网格布局以后，容器子元素（项目）的 float、display: inline-block、display: table-cell、vertical-align 和 column-\*等设置都将失效
- grid-template-columns 定义每一列的列宽
- grid-template-rows 定义每一行的行高
- repeat 重复赋值
- auto-fill 如果希望每一行（或每一列）容纳尽可能多的单元格，这时可以使用 auto-fill 关键字表示自动填充。grid-template-columns: repeat(auto-fill, 100px)
- fr 表示比例关系
- minmax 长度范围
- auto 浏览器自己决定长度
- 网格线的名称 指定每一根网格线的名字，方便以后的引用
- grid-row-gap，grid-column-gap，grid-gap 行间距，列间距，同时设置
- grid-template-areas 一个区域由单个或多个单元格组成。如果某些区域不需要利用，则使用"点"（.）表示
- grid-auto-flow 默认值是 row，即"先行后列"。也可以将它设成 column，变成"先列后行"
- justify-items 单元格内容的水平位置
- align-items 单元格内容的垂直位置
- place-items align-items 属性和 justify-items 属性的合并简写形式
- justify-content align-content place-content

### 生成器

- https://vue-grid-generator.netlify.app/
- https://cssgrid-generator.netlify.app/
- https://grid.layoutit.com/
- https://css-grid-layout-generator.pw/
