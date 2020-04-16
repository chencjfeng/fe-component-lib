# 步骤条-step

## 样式

<img src="https://gph.is/g/E3njRJO" alt="step" style="zoom:50%;" />

## 参数-Attributes

|      参数      |     说明     |                 类型                 | 可选值 |         默认值         |
| :------------: | :----------: | :----------------------------------: | :----: | :--------------------: |
|      data      | 步骤条数据源 | Array({value: string; key: number;}) |   -    |           []           |
| value/ v-model |    绑定值    |    {value: string; key: number;}     |   -    | { key: -1, value: '' } |
|  normalColor   |  默认背景色  |                String                |   -    |        #42b983         |
|  heightColor   |  高亮背景色  |                String                |   -    |        #229963         |
|   arrowColor   |   箭头颜色   |                String                |   -    |        #ffffff         |
|   arrowWidth   |   箭头宽度   |                Number                |   -    |           4            |
| stepItemWidth  |  步骤条宽度  |                Number                |   -    |          150           |
|   textColor    |   文字颜色   |                String                |   -    |        #ffffff         |



## 事件-Events

| 事件名称  |         说明         |                     回调参数                      |
| :-------: | :------------------: | :-----------------------------------------------: |
| stepClick | 步骤点击时触发的事件 | 点击中的step值，类型{value: string; key: number;} |

