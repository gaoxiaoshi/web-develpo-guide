# 迅睿CMS系统学习文档

迅睿CMS系统是一款基于CodeIgniter框架的免费、简洁、高效、灵活的PHP内容管理系统，为您的网站提供一个完美的开源解决方案。

## 一、安装使用
#### 1. 安装环境
###### 1.1 系统环境

1）如果电脑内存有16G，强烈建议使用centos7的虚拟机安装宝塔面板来配置环境，这样会更加接近生产，避免环境不一造成的兼容性问题，虚拟机推荐：
MAC端：Parallels Desktop 15 for Mac (可以用试用版或者找PJ版)
WIN端：VMware Workstation（直接官网下载，然后百度找激活码）
2）如果电脑配置不够可以是用集成环境：
MAC端：MAMP Pro for Mac (可以用试用版或者找PJ版)
WIN端：phpstudy 8.0（免费应用，官网自行下载）

###### 1.2 软件环境

```
PHP 7.2+
MySql 5.6+
```

#### 2. 安装步骤

<font color=#FF0000 >注：如果是在CENTOS虚拟机中安装，上传文件一定要使用ftp方式上传，不要用sftp，会造成文件权限过高，不仅影响安全性，还有可能导致程序出现无法预知的问题。</font>
<video src="https://file.xunruicms.com/video/迅睿CMS安装.mp4" style="width: 100%; height: 100%;" controls="controls"></video>

#### 3. 目录结构

```
|
|-- api                                            // 接口调用入口、编辑器等
|-- cache                                        // 缓存文件目录，可自定义位置
|-- config                                        // 用户的一些自定义配置、自定义函数、自定义钩子等
|-- dayrui                                        // 系统核心程序目录
|    |-- App                                      // 应用程序目录、自定义应用、自定义插件、自定义模型
|    |-- Core                                     // 迅睿CMS项目目录
|    |-- Fcms                                    // 迅睿CMS程序类目录
|    |-- System                                 // CodeIgniter框架目录
|-- mobile                                       // 移动端主入口文件夹
|-- static                                         // 静态资源目录
|    |-- assets                                   // 全局静态资源
|    |-- default                                 // 默认模板静态资源
|    |-- custom                                 // 自定义模板静态资源目录（可以根据实际网站名称自定义）
|-- template                                    // 模板目录
|    |-- mobile                                  // 移动端模板
|    |-- pc                                         // PC端模板
|         |-- default                             // PC端默认模板目录
|         |-- custom                             // 自定义模板目录（可以根据实际网站名称自定义）
|-- uploadfile                                    // 附件上传目录
|-- admin.php                                   // 后台主入口
|-- index.php                                    // 前端主入口
|-- install.php                                   // 系统安装主入口，正式部署时需要删除该文件
|
```

#### 4. 数据表说明

详情见后台->系统->系统维护->数据字典

## 二、后台操作
#### 1. 设置板块
#### 2. 内容板块
## 三、模板开发
#### 1. 模板定义
1. 模板目录
2. 模板关联（后台添加栏目）

#### 2. 模板语法
###### 2.1 模板引用
1）引用本目录下的xxx.html，当本目录不存在时会引用主目录下的xxx.html
```
{template "xxx.html"}
```
2）强制引用主目录下的xxx.html
```
{template "xxx.html", "/"}
```
###### 2.2 变量、常量、数组
遵循php的语法
1）变量
```
{$变量名}

例1、输出变量
{$test}表示输出test变量

例2、变量计算
{$test+1}表示test变量加了一个1，再输出
```
2）常量
```
{大写字母}
常量是固定的值，输出常量{SITE_URL}
```
3）数组
```
{$数组名[键1]}、{$数组名[键1][键2]}、...
```
4）简易数组
```
{$数组名.键1}、{$数组名.键2} （最多支持3级，最好直接输出）
```
###### 2.3 判断语句
```
// 支持的运算符：> 、< 、>= 、<=、==、!= 、<> 
{if $模板变量1 运算符 $模板变量2}
   模板内容1
{else if $模板变量1 运算符 $模板变量3}
   模板内容2
{else}
   模板内容3
{/if}
```
#### 3. 模板常用变量
详情请见官方说明文档：[模板变量](https://www.xunruicms.com/doc/mobanbianliang.html)
###### 网站首页常用变量
| 变量代码 | 说明 |
| --- | --- |
| {$meta_title} | 页面头部标题 |
| {$meta_keywords} | 页面头部关键字，采用网站关键字 |
| {$meta_description} | 页面头部描述，采用网站描述 |
| {$indexc} | 用于判断是否是首页 |

#### 4. 模板常用标签
详情请见官方说明文档：[标签调用](https://www.xunruicms.com/doc/biaoqiandiaoyong.html)，这里只对比较常用的标签做一些简单的整理，具体使用可以看官方的模板
###### 4.1 导航栏调用
```
<!--调用共享栏目-->
<!--第一层：调用pid=0表示顶级-->
{category module=share pid=0}
	<li class="menu-dropdown classic-menu-dropdown {if IS_SHARE && $catid && in_array($catid, $t.catids)} active{/if}">
		<a href="{$t.url}" title="{$t.name}" {if $t.tid==2} target="_blank"{/if}>{$t.name}</a>
		{if $t.child}
		<ul class="dropdown-menu pull-left">
			<!--第二层：调用第二级共享栏目-->
			{category module=share pid=$t.id return=t2}
			<li class="{if $t2.child} dropdown-submenu{/if} {if IS_SHARE && $catid && in_array($catid, $t2.catids)} active{/if}">
				<a href="{$t2.url}" class="nav-link nav-toggle " title="{$t2.name}">{$t2.name}</a>
				{if $t2.child}
				<ul class="dropdown-menu pull-left">
					<!--第三层：调用第三级共享栏目数据-->
					{category module=share pid=$t2.id return=t3}
					<li class="{if IS_SHARE && $catid && in_array($catid, $t3.catids)} active{/if}">
						<a href="{$t3.url}" title="{$t3.name}">{$t3.name}</a>
					</li>
					{/category}
				</ul>
				{/if}
			</li>
			{/category}
		</ul>
		{/if}
	</li>
{/category}
```
###### 4.2 任意模块的数据调用，[官方文档](https://www.xunruicms.com/doc/15.html)

```
<!--在首页调用新闻模块下的数据-->
{module module=news order=updatetime num=9}
链接地址：{$t.url}
新闻标题：{$t.title} 或者 {dr_strcut($t.title, 20)}（不建议）
缩略图片：{dr_thumb($t.thumb, 宽, 高, 是否水印)} 或者原图 {dr_get_file($t.thumb)}
发布时间：{$t.updatetime} 或者 {dr_date($t._updatetime, 'Y-m-d')}
{/module}
```
###### 4.3 列表页数据调用
这里使用的方法其实和4.2一样，多了两个参数catid（当前栏目ID）和page（分页）
```
{module catid=$catid order=updatetime page=1}
{/module}
<!--分页代码，样式修改位置config/page/pc/page.php-->
{$pages}
```
## 四、经验分享
#### 1. 开发时使用正式域名
#### 2. 列表循环时使用序号
```
{$key+1}
```