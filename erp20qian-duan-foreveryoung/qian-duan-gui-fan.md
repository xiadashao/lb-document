\#\#\# 命名规范

+ 组件命名规范： 帕斯卡命名法\(所有首字母大写\)

+ 注册组件名规范： 帕斯卡命名法\(所有首字母大写\)

+ 路由命名规范： 驼峰命名法

+ 函数命名规范：

  + 卡片dialog图标点击事件： action前缀：

    \`\`\`

    // 为了跟 action 属性对应，使用 action 前缀

    dialogPanel2Icons: \[

      {

        fCls: 'el-icon-close',

        tip: '关闭',

        type: 'close',

        action: \(done\)=&gt; {

          this.actionPanel2Close\(\);

          done\(\);

        }

      },

    \]

    \`\`\`

  + 绑定事件: handle前缀 \[其他可选 bind\]

  + 网络请求相关事件 req前缀 eg: reqGetXXX  reqSaveXXX





\#\#\# js规范

+ 组件根据业务需要提供初始化方法，用来统一重新刷新页面 eg:initPageStatus





\#\#\# 样式规范

+ 组件样式必须加scoped\(除脱离组件的样式\)，并且使用顶级元素类名作为约束

  \`\`\`

  &lt;style lang="stylus" scoped&gt;

  	.manager-index {

      height: 100%;

  	}

  &lt;/style&gt;

  \`\`\`

