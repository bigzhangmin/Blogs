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

页面

* 邮件的宽度一般在**600-800**不等，具体宽度由UI制定，正常不超过**800**
* 可以使用`HTML`常用标签，不支持`H5`规范
* 支持`CSS3`之前的样式，`CSS3`部分支持但**不推荐**使用，邮件内只能写行内样式，部分邮件代发工具可写内联样式并支持hover效果
* 布局严格使用`table`表格格式，否则在邮件中可能会显示会发生异常，也会加大邮件被墙的几率
* 内侧边或者上下有空白间距，尽量不要用 padding，必须得用标准的` td `来设定空白间距，否则会导致各个邮箱解析不同
* 关于样式继承，每个邮件平台标准都不一样，所以尽量少用样式继承，尽管这会增加更多代码使`HTML`结构看起来混乱
* 合并单元格：`colspan="3"` （将3行合并为一行）
* 正常项目中我们会避免标签嵌套太深，但在邮件中必须使用表格嵌套，所以经除会看到嵌套十多层标签也是正常的。但需要注意避免出错。

```html
    <!-- Outside the container -->
    <table width="100%" cellpadding="0" cellspacing="0" border="0" style="margin:0 auto; border-spacing:0; border-collapse:collapse;">
        <tbody>
            <tr>
                <td style="padding: 0;">
                    <!-- Inside the container -->
                    <table align="center" width="750" border="0" cellspacing="0" cellpadding="0" style="width:750px;max-width: 750px;table-layout:fixed;border-collapse:collapse;background-color: #ffffff;">
                        <tbody>
                            <!-- Header area -->
                            <tr>
                                <td>
                                    <table width="100%" border="0" cellspacing="0" cellpadding="0" style="border-spacing:0; border-collapse:collapse;padding-top: 20px;">
                                        <tbody>
                                            <tr>
                                                <td></td>
                                            </tr>
                                        </tbody>
                                    </table>
                                </td>
                            </tr>
                            <!-- Content area -->
                            <tr>
                                <td>
                                    <table width="100%" border="0" cellspacing="0" cellpadding="0" style="border-spacing:0; border-collapse:collapse">
                                        <tbody>
                                            <tr>
                                                <td></td>
                                            </tr>
                                        </tbody>
                                    </table>
                                </td>
                            </tr>
                            <!-- Footer area -->
                            <tr>
                                <td>
                                    <table width="100%" border="0" cellspacing="0" cellpadding="0" style="border-spacing:0; border-collapse:collapse">
                                        <tbody>
                                            <tr>
                                                <td></td>
                                            </tr>
                                        </tbody>
                                    </table>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </td>
            </tr>
        </tbody>
    </table>
```

完整模板下载：<a href="#" download="email-template.html">EDM邮件模板</a>