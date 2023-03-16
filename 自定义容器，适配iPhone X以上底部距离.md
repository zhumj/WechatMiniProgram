## ZContainer.wxss

```
.z_container {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
}

.z_container__content {
  flex: 1;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}
```

## ZContainer.wxml

```
<view class="z_container">
  <view class="z_container__content" style="margin-bottom: {{iphoneBottomLift}}px;">
    <slot></slot>
  </view>
</view>
```

## ZContainer.ts

```
Component({
  /**
    * 组件的属性列表
    */
  properties: {

  },

  /**
    * 组件的初始数据
    */
  data: {
    iphoneBottomLift: 0
  },

  /**
    * 组件的方法列表
    */
  methods: {

  },

  lifetimes: {
    ready() {
      wx.getSystemInfo().then((res) => {
        this.setData({
            iphoneBottomLift: res.screenHeight - res.safeArea.bottom
        })
      })
    }
  }
})
```

# 使用

- 在 app.wxss 定义全局 page 标签

```
page {
  width: 100%;
  height: 100%;
}
```

- 然后在 app.json 中加载组件，这样加载进来是全局组件，其它页面直接使用就行了

```
{
  "pages": [
    ...
  ],
  
  "window": {
    ...
  },
  "usingComponents": {
    "z-container": "./components/z-container/ZContainer"
  },
  "style": "v2",
  "sitemapLocation": "sitemap.json"
}
```