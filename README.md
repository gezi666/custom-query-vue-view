# 可视化自定义查询条件

## 依赖

    Vue 2.6.10+、ElementUI 2.10.1+（具体为：Input、Cascader、CascaderPanel、Select、Option、Button、Icon组件）

## 特点：

1、 支持增加/删除条件、条件块，并设置连接关系；

2、 支持根据指标列所选指标动态扩展指标列；

3、 支持根据指标列所选指标动态设置条件行的比较值可选下拉/级联选项；

4、 支持获取当前设置的自定义查询条件；

5、 支持反显查询条件。

![效果图](https://raw.githubusercontent.com/gezi666/pictureBed/main/pictures/custom-query-vue.png)

## 安装

```
npm install custom-query-vue -S
```

## 快速上手

```
// 安装插件
import CustomQuery from 'custom-query-vue'

Vue.use(CustomQuery)


// 使用组件
<custom-query
  ref="customQuery"
  :quotaList="quotaList"
  @conditionChange="conditionChange"
/>
```

## 属性/方法

```
1、quotaList 为第一指标列的下拉选项列表；
	格式：[
		{
			label: "",  // 显示值
			value: "", // 选项值，格式可为任意类型
			children:[ // 如果选项有级联下级，若无可省略
				{
					label: "",  // 显示值
					value: "", // 选项值，格式可为任意类型
				}
			]
		}
	]

2、@conditionChange 为指标列值发生变化时触发，返回：{context,value}
	context：当前条件行实例
	value：当前选择的指标值

3、新增指标列，context为指标值发生变化时触发方法返回的context
	context.addQuotaColumn([
		{
			label: "",  // 显示值
			value: "", // 选项值，格式可为任意类型
			children:[ // 如果选项有级联下级，若无可省略
				{
					label: "",  // 显示值
					value: "", // 选项值，格式可为任意类型
				}
			]
		}
	])

4、设置条件行比较值的下拉可选项，context为指标值发生变化时触发方法返回的context
	context.setCompareOptions([
		{
			label: "",  // 显示值
			value: "", // 选项值，格式可为任意类型
		}
	],cascaderProps)

	cascaderProps参数可以设置级联下拉属性，具体参考文档最后链接


5、获取当前自定义查询条件
	this.$refs.customQuery.getCustomQuery()

	// 返回数据格式
	{
		connectRelation:"and", // 连接条件 and-且,or-或
		conditions:[
			{  // 条件行格式
				quota: "", // 条件行第一指标列值
				addQuotaArr: [ // 新增指标列数组
					{
						quotaValue:"", // 选择的指标值
						options:[  // 指标选项列表
							{
								label:"", // 显示值
								value:"",  // 下拉选项的值可为任意类型
								children:[ // 如果选项有级联下级，若无可省略
									{
										label: "",  // 显示值
										value: "", // 选项值，格式可为任意类型
									}
								]
							}
						]
					}
				],
				condition1: "", // 比较条件
				condition2: "", // 截取时比较条件
				startIndex: "", // 从第几位开始截取
				sliceLength: "", // 截取长度
				startValue: "", // 区间起始值
				endValue: "", // 区间截止值
				compareValue: "", // 条件行需要比较的值
				compareSelectValue: [], // 条件行需要比较的值(级联选择的值)
				compareOptions: [ // 条件行需要比较的值的下拉可选项
					{
						label: "",  // 显示值
						value: "", // 选项值，格式可为任意类型
					}
				]
			},
			{ // 条件块格式
				connectRelation:"and",
				conditions:[
					{
						quota: "",
						addQuotaArr: [],
						condition1: "",
						condition2: "",
						startIndex: "",
						sliceLength: "",
						startValue: "",
						endValue: "",
						compareValue: "",
						compareSelectValue: [],
						compareOptions: []
					}
					...
				]
			}
			...
		]
	}

6、反显自定义查询条件  queryData格式同上
	this.$refs.customQuery.setCustomQuery(queryData)

```

### cascaderProps 级联选择器属性，具体参考：[Element Cascader 级联选择器组件 Props 属性](https://element.eleme.cn/#/zh-CN/component/cascader#props)

## 捐赠

创作不易，如果您觉得这个插件对您有所帮助，可以请穷匮潦倒的书生吃顿饭。

![捐赠码](https://github.com/gezi666/pictureBed/blob/main/pictures/pay.png?raw=true)
