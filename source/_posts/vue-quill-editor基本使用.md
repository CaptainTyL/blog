---
title: vue-quill-editor基本使用
date: 2023-03-22 10:38:53
tags: vue工具
---

##### Quill.js 富文本（vue-quill-editor）

最近在做一个富文本编辑器，在网上对比找了一圈，选择了[Quill.js](https://www.kancloud.cn/liuwave/quill/1409423)，这是一款偏向底层，易于扩展的富文本编辑器，但是对于新手不太友好，目前来说这个库我自己也没有进行深入的使用和研究，因为目前项目主要以 vue 的为主，所以这次选择了对这个库进行过二次封装的[vue-quill-editor](https://github.com/surmon-china/vue-quill-editor)组件。不过在这次的使用也遇到一些问题。在这里记录一下

###### 1.安装 vue-quill-editor

```javascript
npm install vue-quill-editor --save
```

###### 2.针对 vue-quill-editor 在进行组件的二次封装

vue-quill-editor 封装中的说明：

1.在样式中对原有样式中有英文描述的使用中文进行覆盖

2.引入组件的同时 需要将 quill 的样式文件也进行引入

```javascript
<template>
  <div>
    <quill-editor
      class="editor"
      :content="content"
      :options="editorOption"
      ref="myQuillEditor"
      @change="onEditorChange($event)"
    >
    </quill-editor>
  </div>
</template>
<script>
import "quill/dist/quill.core.css";
import "quill/dist/quill.snow.css";
import "quill/dist/quill.bubble.css";
import { quillEditor } from "vue-quill-editor";

const toolbarOptions = [
  ["bold", "italic", "underline", "strike"], // 加粗 斜体 下划线 删除线
  ["blockquote", "code-block"], // 引用  代码块
  [{ header: 1 }, { header: 2 }], // 1、2 级标题
  [{ list: "ordered" }, { list: "bullet" }], // 有序、无序列表
  [{ script: "sub" }, { script: "super" }], // 上标/下标
  [{ indent: "-1" }, { indent: "+1" }], // 缩进
  // [{'direction': 'rtl'}],                         // 文本方向
  [{ size: ["small", false, "large", "huge"] }], // 字体大小
  [{ header: [1, 2, 3, 4, 5, 6, false] }], // 标题
  [{ color: [] }, { background: [] }], // 字体颜色、字体背景颜色
  [{ font: [] }], // 字体种类
  [{ align: [] }], // 对齐方式
  ["clean"], // 清除文本格式
  ["link", "image", "video"], // 链接、图片、视频
]; //工具菜单栏配置

export default {
  props:{
    content: {
      type: String,
      default: ''
     }
   },
  components: {
    quillEditor,
  },
  data() {
    return {
      editorOption: {
        modules: {
          toolbar: {
            container: toolbarOptions,
            handlers: {},
          },
        },
        placeholder: "请输入内容......",
        readOnly: false,
        theme: "snow", //主题 snow/bubble
      },
    };
  },
  methods: {
    // 富文本组件change事件
    onEditorChange({ quill, html, text }) {
      this.$emit("editorChange", html);
    },
  },
};
</script>
<style lang="scss">
.editor {
  line-height: normal !important;
  height: 590px;
  .ql-container {
    height: 500px !important;
    border: 1px solid #ebebeb !important;
    border-bottom-left-radius: 4px;
    border-bottom-right-radius: 4px;
    border-top: 0 !important;
  }
  .ql-toolbar {
    border: 1px solid #ebebeb !important;
    border-top-left-radius: 4px;
    border-top-right-radius: 4px;
  }
  .ql-snow .ql-tooltip[data-mode="video"] {
    left: 112px !important;
  }
  .ql-snow .ql-tooltip[data-mode="video"]::before {
    content: "请输入视频地址:";
  }
  .ql-tooltip[data-mode="link"]::before {
    content: "请输入链接地址:";
  }
  .ql-snow .ql-tooltip[data-mode="link"] {
    left: 112px !important;
  }
  .ql-formats {
    > .ql-picker.ql-size {
      .ql-picker-label::before {
        content: "14px";
      }
      .ql-picker-item::before {
        content: "14px";
      }
      .ql-picker-label[data-value="small"]::before {
        content: "10px";
      }
      .ql-picker-item[data-value="small"]::before {
        content: "10px";
      }
      .ql-picker-label[data-value="large"]::before {
        content: "18px";
      }
      .ql-picker-item[data-value="large"]::before {
        content: "18px";
      }
      .ql-picker-label[data-value="huge"]::before {
        content: "32px";
      }
      .ql-picker-item[data-value="huge"]::before {
        content: "32px";
      }
    }
    > .ql-picker.ql-header {
      .ql-picker-label::before {
        content: "文本";
      }
      .ql-picker-item::before {
        content: "文本";
      }
      .ql-picker-label[data-value="1"]::before {
        content: "标题1";
      }
      .ql-picker-item[data-value="1"]::before {
        content: "标题1";
      }
      .ql-picker-label[data-value="2"]::before {
        content: "标题2";
      }
      .ql-picker-item[data-value="2"]::before {
        content: "标题2";
      }

      .ql-picker-label[data-value="3"]::before {
        content: "标题3";
      }
      .ql-picker-item[data-value="3"]::before {
        content: "标题3";
      }

      .ql-picker-label[data-value="4"]::before {
        content: "标题4";
      }
      .ql-picker-item[data-value="4"]::before {
        content: "标题4";
      }
      .ql-picker-label[data-value="5"]::before {
        content: "标题5";
      }
      .ql-picker-item[data-value="5"]::before {
        content: "标题5";
      }
      .ql-picker-label[data-value="6"]::before {
        content: "标题6";
      }
      .ql-picker-item[data-value="6"]::before {
        content: "标题6";
      }
    }
    > .ql-picker.ql-font {
      .ql-picker-label::before {
        content: "标准字体";
      }
      .ql-picker-item::before {
        content: "标准字体";
      }
      .ql-picker-label[data-value="serif"]::before {
        content: "衬线字体";
      }
      .ql-picker-item[data-value="serif"]::before {
        content: "衬线字体";
      }
      .ql-picker-label[data-value="monospace"]::before {
        content: "等宽字体";
      }
      .ql-picker-item[data-value="monospace"]::before {
        content: "等宽字体";
      }
    }
  }
}
</style>
```

###### 3.图片上传方法的重写

原因：编辑器本身是可以进行图片上传的 不过上传的图片都是转换成 base64 放上去的。这样会导致整个编辑器输出的 html 文本过大， 提交后台接口失败。

解决方法：让用户在使用上传图片的时候 直接将图片上传到服务器 然后使用返回的 url 链接放入富文本的内容中 ，因为我当前 vue 项目是使用 element 组件库 所以下面选择使用 element 中的 upload 组件 进行辅助上传

- 组件内使用 element upload 组件

  ```javascript
  <template>
    <div>
      <!-- 使用element图片上传组件 将其隐藏主要用于辅助富文本组件上传图片 -->
      <el-upload
        class="editor-uploader"
        :action="uploadPath"
        :multiple="false"
        :show-file-list="false"
        :on-success="uploadSuccess"
        :before-upload="beforeUpload"
        v-show="false"
      >
      </el-upload>
      <quill-editor
        class="editor"
        :content="content"
        :options="editorOption"
        ref="myQuillEditor"
        @change="onEditorChange($event)"
      >
      </quill-editor>
    </div>
  </template>
  ```

- 使用 handlers 重写图片上传方法，定义编辑器中图片上传按钮事件

  ```javascript
   handlers: {
      image: (value) => {
         if (value) {
            // 调用 element 上传组件
            document.querySelector(".editor-uploader input").click();
           } else {
            this.quill.format("image", false);
             }
       },
    },
  ```

- 图片上传组件的拦截方法实现和成功后的写入操作

  ```javascript
     //图片上传之前限制
      beforeUpload(file) {
        const isImage = file.type.indexOf("image/") > -1;
        const isLt1M = file.size / 1024 / 1024 < 1;
        if (!isImage) {
          this.$message.error("仅支持上传图片!");
        } else if (!isLt1M) {
          this.$message.error("请将图片大小控制在1MB内!");
        }
        return isImage && isLt1M;
      },
      //图片上传成功
      uploadSuccess(res, file, fileList) {
        // 获取富文本示例
        let quill = this.$refs.myQuillEditor.quill;
        if (res.flag) {
          // 获取光标所在的位置
          let length = quill.getSelection().index;
          // 插入图片
          quill.insertEmbed(length, "image", res.data.url);
          // 调整光标在图片之后
          quill.setSelection(length + 1);
        } else {
          this.$message.error("图片上传失败！");
        }
      },
  ```

###### 4.图片缩放处理

- 安装富文本编辑器内图片缩放模块

```javascript
npm install quill-image-resize-module --save
```

- 引入图片缩放模块

```javascript
import { quillEditor, Quill } from "vue-quill-editor";

// 引入图片缩放模块 并注册到Quill上
import ImageResize from "quill-image-resize-module";
Quill.register("modules/imageResize", ImageResize);
```

- 在 vue-quill-editor 配置中模块下 加入缩放模块

```javascript
  editorOption: {
        modules: {
          // 图片缩小放大插件配置
          imageResize: {
            displaySize: true,
          },
         // ...省略其他配置
      },
```

使用图片缩放模块的注意点，在使用过程中遇到了一个报错，发现是还需要在 webpack 中加入配置 该模块才可以引入成功 继而正常使用

报错问题 **<mark>Cannot read property 'imports' of undefined"</mark>**

1. 使用 webpack 打包的项目

在 build 文件夹下找到 webpack.base.conf.js 文件 在 plugins 中加入如下代码

```javascript
//若文件中未引入 webpack 则需
const webpack = require("webpack");

// 在webpack插件中引入Quill.js文件
plugins: [
  new webpack.ProvidePlugin({
    "window.Quill": "quill/dist/quill.js",
    Quill: "quill/dist/quill.js",
  }),
];
```

2.使用 vue-cli 脚手架搭建的项目

在 vue.config.js 中进行设置

```javascript
//若文件中未引入 webpack 则需
const webpack = require("webpack");

module.exports = {
  chainWebpack: (config) => {
    config.plugin("provide").use(webpack.ProvidePlugin, [
      {
        "window.Quill": "quill/dist/quill.js",
        Quill: "quill/dist/quill.js",
      },
    ]);
  },
};
```
