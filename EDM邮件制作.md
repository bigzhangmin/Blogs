## EDM邮件制作

EDM营销（Email Direct Marketing）也叫：Email营销、电子邮件营销。是指企业向目标客户发送EDM邮件，建立同目标顾客的沟通渠道，向其直接传达相关信息，用来促进销售的一种营销手段。也可用于发送邮件广告、产品信息、销售信息、市场调查、市场推广活动信息等。



### 1. 清除表格默认样式

> 如果你对`<table>`的[相关属性](https://www.w3school.com.cn/tags/tag_table.asp)不太了解，建议先了解一下它常用的一些[属性](https://www.w3school.com.cn/tags/tag_table.asp)。

**table**标签用来定义一个表格，无论是在邮件中还是在不同浏览器中，**table**标签都带有默认的间距以及一些不能被**Style**覆盖的属性，在页面清除相对简单一行**CSS**就搞定，但在邮件中我们只能写行内样式，所以需要给`<table>`加上以下属性和样式。

```html
<table cellpadding="0" cellspacing="0" border="0" style="border-spacing:0; border-collapse:collapse;table-layout:fixed;">
    <tr>
    	<td style="padding: 0;">
        	<!-- 嵌套表格也需要清除样式 -->
            <table cellpadding="0" cellspacing="0" border="0" style="border-spacing:0; border-collapse:collapse;table-layout:fixed;"></table>
        </td>
    </tr>
</table>
```

> 这里有一个需要注意的地方，如果要在`<table>`上使用`padding`需要将`border-collapse: collapse`去除，否则不能使用`padding`。

| 属性                      | 功能                                         |
| :------------------------ | :------------------------------------------- |
| cellpadding="0"           | 单元格边距为0                                |
| cellspacing="0"           | 单元格间距为0                                |
| border="0"                | 边框大小为0                                  |
| border-spacing: 0         | 边框间距为0                                  |
| border-collapse: collapse | 用于表格属性，表示表格的两边框合并为一条     |
| table-layout: fixed;      | 固定表格布局，允许浏览器更快地对表格进行布局 |

### 2. 格式

1. 邮件的宽度一般在**600px**到**800px**不等，具体宽度由设计师制定，正常不超过**800px**。

2. `HTML`编码使用**utf-8**。

3. 布局应严格使用`table`表格布局，否则在邮件中显示可能会发生异常，也会加大邮件被墙的几率。

4. 严格来说邮件不支持使用外链样式以及内联样式，仅能使用行内样式，像这样：

   ```html
   <td style="font-family: serif;font-size: 16px;color: #ccc;">Text</td>
   ```

   关于样式继承，不同邮箱平台解析标准不同，部分继承样式可能会失效，所以应当减少使用样式继承，虽然这会增加更多的样式代码。

   目前已有许多邮件发送工具支持使用内联样式，可以在`<style></style>`标签中编写**CSS**，支持**Class**、一般选择器、**hover**效果等，使用内联样式前请务必确认邮件发送工具支持编写内联样式，接受邮箱也支持，否则邮件中的样式会丢失。

   ```html
   <style>
   	.normal-text{
   		font-family: serif;
   		font-size: 16px;
   		color: #ccc;
   	}
   	.hover-bule:hover{
   		color: bule;
   	}
   </style>
   
   <td class="normal-text">
   	Text
   	<p class="hover-bule">hover change font color</p>
   </td>
   ```

5. 内边距和外边距尽量不适用`padding`和`margin`，正确的做法是使用空标签来设定间距，否者会导致各个邮箱平台解析不同，造成差异。注意：使用`padding`请先去掉`<table>`上的`border-collapse:collapse`样式，或者将值改为`border-collapse: unset`。

6. 表格居中可使用`align="center"`属性，加在`<table>`标签上。合并单元格(td)可使用`colspan="3"`属性。

7. 一般项目中我们会避免深层嵌套，但邮件中使用表格布局免不了深层嵌套，所以有些嵌套十多层标签也不足为奇。但需要注意避免搞混。



完整模板下载：<a href="#" download="email-template.html">EDM邮件模板</a>