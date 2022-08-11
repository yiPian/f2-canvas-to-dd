# uni-app开发钉钉小程序 引入的F2组件

是将[my-f2](https://github.com/antvis/my-f2)内的逻辑提取出来，组装成uni-app里面的自定义组件。

## 如何使用

### 1.将此项目文件放置到根目录 *mycomponents* 文件下

|- mycomponents

    |- f2-canvas-to-dd

        |- lib

        |- f2-canvas.acss

        |- f2-canvas.axml

        |- f2-canvas.js
        
        |- f2-canvas.json

### 2.使用组件

```vue
<template>
    <view>
        <f2-canvas :on-init="onInitChart" :width="300" :height="300"></f2-canvas>
    </view>
</template>

<script>
    import F2Canvas from '@/mycomponents/f2-canvas-to-dd/f2-canvas'

    export default {
        components: { F2Canvas },
        methods: {  
            onInitChart(F2, config) {
                const chart = new F2.Chart(config);
                const data = [
                { value: 63.4, city: 'New York', date: '2011-10-01' },
                { value: 62.7, city: 'Alaska', date: '2011-10-01' },
                { value: 72.2, city: 'Austin', date: '2011-10-01' },
                { value: 58, city: 'New York', date: '2011-10-02' },
                { value: 59.9, city: 'Alaska', date: '2011-10-02' },
                { value: 67.7, city: 'Austin', date: '2011-10-02' },
                { value: 53.3, city: 'New York', date: '2011-10-03' },
                { value: 59.1, city: 'Alaska', date: '2011-10-03' },
                { value: 69.4, city: 'Austin', date: '2011-10-03' },
                ];
                chart.source(data, {
                date: {
                    range: [0, 1],
                    type: 'timeCat',
                    mask: 'MM-DD'
                },
                value: {
                    max: 300,
                    tickCount: 4
                }
                });
                chart.area().position('date*value').color('city').adjust('stack');
                chart.line().position('date*value').color('city').adjust('stack');
                chart.render();
                // 注意：需要把chart return 出来
                return chart;
            }
        }
    }
</script>
```

### 注意不要使用json文件引入组件，会报错。

```json
{
  "usingComponents": {
    "F2Canvas": "/mycomponents/f2-canvas-to-dd/f2-canvas"
  }
}
```