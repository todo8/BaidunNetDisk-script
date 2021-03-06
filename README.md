# 导出百度网盘_共享的文件库文件清单 油猴脚本

## todo
- [ ] 保存下载记录，避免重复性下载
- [ ] 保存爬取记录，不用重复爬目录
- [ ] 下载指定后缀格式的文件，
- [ ] 保存文件在自己的百度云盘账号，方便百度网盘下载，开通会员可以提高下载速度
- [ ] 直接触发百度网盘下载，
- [ ] 过滤特殊目录，有的目录包含大量无关文件。

## 说明
虽然自己的网盘，有导出目录的工具，但是很多用户间分享的网盘数据，动辄10T 20T，不可能都转存到自己的网盘中。而且转存也有文件数量限制等。
现在买网盘资源，基本都是这种分享方式，而不是卖账号。
因此，分享的网盘资源，里面到底有些什么内容，其实很不方便查看

搜索了一圈，没有现成的方案，大家都在关注如何加速下载等，github上虽然百度网盘相关项目有近百个，但是没有专门导出目录信息的项目。 而且主要都还是针对自己的网盘文件，这种在群中分享的网盘资源，没有现成的访问方法。
没办法，大佬们不关注这个需求，只能自己动手了。
在参考了github中的相关项目，比较了多种技术手段（python脚本，java程序，go语言，油猴脚本）后，本人使用油猴脚本方式来实现这个功能。
功能设计： 导出分享文件库的所有目录和文件内容清单，同时对文件夹内的文件数量和尺寸进行递归统计。

针对百度网盘的油猴脚本，可导出百度网盘共享文件库目录清单
chrome浏览器+油猴脚本测试通过
油猴脚本怎么用我就不写了，请自行百度。 下面写写脚本用法
1 油猴插件中启用本脚本

![](https://pic2.zhimg.com/80/v2-cf86151980da94ccf77dc0a1074a4c0b_hd.jpg?raw=true)

2 百度网盘PC程序，好友分享界面，点击要导出的共享会话，点击文件库. （如果chrome设为缺省浏览器，这时会在浏览器中显示文件库）

![](https://pic4.zhimg.com/80/v2-67476b46d68c4f78fd9811989cbfab02_hd.jpg?raw=true)

3 chrome浏览器中，百度网盘文件库界面，会多出一个”导出目录信息“的按钮。（油猴插件和本脚本都正确加载）

![](https://pic4.zhimg.com/80/v2-5bf2d226f8200517038f58a07c5ec448_hd.jpg?raw=true)

如图，先选择要导出的文件夹，可以单选，可以多选，可以全选，然后点击按钮开始生成清单

4 接下来就是等待，不要关闭页面，清单生成速度同你要导出数据有多少个子目录有关。很多分享的网盘内部文件非常多，等待时间会比较长，大概8000个子目录，需要1个多小时。
清单生成完成后，会弹出文件保存对话框，你可以选择保存到本机目录

![](https://pic1.zhimg.com/80/v2-e79fb6c904f29ad0e87ad56579e8d3b5_hd.jpg?raw=true)

建议先找一个子文件夹少的目录，试用试用，可以很快出结果。免得等几个小时没结果认为我忽悠人。

如果想看到进度，按F12打开调试面板，选择Console面板，可以看到取清单的消息在运行。

0.5版本增加了单独导出子目录的功能，增加了2个按钮， “ID” 和“子目录”。 在根目录下选择子文件夹所在目录，点击<ID按钮>获取主目录信息。然后可以进入子目录，选择要导出的子目录进行导出

![](https://pic2.zhimg.com/80/v2-9af2b29c056a40f618bb301ae63c6e91_hd.jpg?raw=true)

5 保存的内容，是文本文件，按照tree命令的输出格式输出，大致如下的样子

![](https://pic2.zhimg.com/80/v2-cda365dc4467ddbfe2290120abc78e1e_hd.jpg?raw=true)

文件夹，下面列出所有子文件及子文件夹，文件夹统计了其整体空间之和，文件单独输出了文件大小。

6 百度网盘的通讯协议还有些复杂，我也就弄了两天，第一次写js和油猴脚本，经验也不足，现在这个程序还有一些不完善之处

第一： 如果一个文件夹下面子文件超过100（不是文件夹包含的所有文件，是直接在该文件夹下面的文件），有可能超过100的文件列不出来。这个问题我还没有专门测试，我也没有这种极端情况，后面有需求时再说

第二：限于现在了解的JS特性，没有用异步请求，所以列表生成比较慢。能否有方法加速，如有js高手可以尝试一下，反正源码都公开了

------------ 2019.7.6 -----------
功能更新
1. 解除一个文件夹只能导出100个子文件限制，可以输出子目录所有文件 （最多3000）
2. 文件前面输出目录的层次信息，方便过滤
3. 文件信息增加输出全路径名

 ----------- 2020.10.26 ----------
 增加单独导出子目录的功能
 简化代码结构
 

 ----------- 2020-11-14 ----------
自动获取导出子目录时用的参数
调用api直接下载文件，并保存原有的文件目录
await优化协议代码，增加可读性。


