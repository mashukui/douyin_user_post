# douyin_user_post
> 马哥原创：爬抖音博主软件v1.5版，一键批量采集对标账号主页作品，包含视频下载和数据采集，包含17个核心字段。

> 本软件工具仅限于学术交流使用，严格遵循相关法律法规，符合平台内容合法合规性，禁止用于任何商业用途！

# 一、背景分析
## 1.1 开发背景与功能介绍

我是 @马哥python说，一枚10年+程序猿，现全职独立开发。

和很多同学聊过，他们希望有一个小工具，把抖音指定博主（对标账号）的主页已发布作品的数据及视频全部采集下来，然后做数据分析使用。为了满足这类需求，我特意用python开发了这款工具：**douyin_user_post**

软件运行界面：![image](https://files.mdnice.com/user/32110/429fb6e8-85c0-4137-8554-3faaba6975e3.jpg)

 
自动导出的作品csv文件：（包含17个字段： 页码,作者昵称,uid,sec_uid,作者链接,作者粉丝数,视频标题,视频标签,视频链接,发布时间,视频时长,是否置顶,点赞数,评论数,收藏数,推荐数,转发数）
![image](https://files.mdnice.com/user/32110/d4a468a3-76f6-427f-81c4-12fd8d0d342d.png)

 
自动存储到文件夹里的视频文件：
![image](https://files.mdnice.com/user/32110/743f5c60-1321-4a70-835e-6a43486a503a.png)

 
视频mp4文件的存储规则：
1. 以博主昵称命名视频文件夹
2. 视频文件夹里存储的视频文件，以视频id命名，比如：7585842009861279011.mp4
3. 如果作品是图文类，则不下载视频

以上。

## 1.2 软件说明
重要说明，请详读：
1. Windows系统、Mac系统均可直接运行，无需配置python环境
2. 软件通过接口协议爬取，并非通过模拟浏览器等RPA类工具，稳定性较高！
3. 软件运行完成后，会在当前文件夹（即，软件所在文件夹）生成csv结果文件
4. 爬取过程中，每爬一条，存一次csv。并非爬完最后一次性保存！防止因异常中断导致丢失前面的数据（每条请求间隔2s，可自由配置）
5. 爬取过程中，有log文件详细记录运行过程，方便回溯

# 二、主要技术
## 2.1 模块介绍

软件全部模块采用python语言开发，主要分工如下：
```python
tkinter：GUI软件界面
requests：爬虫请求
json：解析响应数据
time：间隔等待，防止反爬
csv：保存csv结果
logging：日志记录
```
出于版权考虑，暂不公开完整源码，仅向用户提供软件使用权。

## 2.2 部分源码
软件界面：
```python
# 创建主窗口
root = tk.Tk()
root.title('爬抖音博主软件v1.5 | 马哥python说')
# 设置窗口大小
root.minsize(width=850, height=660)
```
爬虫请求：
```python
# 发送请求
r = requests.get(url, headers=h2, params=params)
# 接收响应数据
json_data = r.json()
```
保存数据：
```python
# 保存到csv文件
with open(self.result_file, 'a+', encoding='utf_8_sig', newline='') as f:
	writer = csv.writer(f)
	writer.writerow(data_row)
self.tk_show('csv已保存：' + self.result_file)
```
日志记录：
```python
def get_logger(self):
	self.logger = logging.getLogger(__name__)
	# 日志格式
	formatter = '[%(asctime)s-%(filename)s][%(funcName)s-%(lineno)d]--%(message)s'
	# 日志级别
	self.logger.setLevel(logging.DEBUG)
	# 控制台日志
	sh = logging.StreamHandler()
	log_formatter = logging.Formatter(formatter, datefmt='%Y-%m-%d %H:%M:%S')
	# info日志文件名
	info_file_name = time.strftime("%Y-%m-%d") + '.log'
	# 将其保存到特定目录
	case_dir = r'./logs/'
	info_handler = TimedRotatingFileHandler(filename=case_dir + info_file_name,
											when='MIDNIGHT',
											interval=1,
											backupCount=7,
											encoding='utf-8')
	self.logger.addHandler(sh)
	sh.setFormatter(log_formatter)
	self.logger.addHandler(info_handler)
	info_handler.setFormatter(log_formatter)
	return self.logger
```
日志文件截图：
![log文件](https://files.mdnice.com/user/32110/d1c9da48-1ee6-4c3e-89d9-f8aa87efeb95.jpg)

 以上。

# 三、演示视频
软件使用过程演示：[【软件演示】抖音主页作品采集工具](https://mp.weixin.qq.com/s/owsDmHGMYjJEaF3inKZhuA)

# 四、付费说明
## 4.1 卡密说明
付费如下：
```python
日卡：使用期限1天，29元。日卡仅能购买一次。适合试用等临时需求
月卡：使用期限1个月，149元。月卡可多次购买。适合短期采集需求
季卡：使用期限3个月，399元。季卡可多次购买。适合中期采集需求
年卡：使用期限1年，799元。年卡可多次购买。适合长期采集需求
```
付费方式：
<img width="2086" height="642" alt="收款码v3" src="https://github.com/user-attachments/assets/a9b619e7-c76f-4c90-b885-d3d10d57abfd" />

付费后，加我微信（493882434）自动掉落登录卡密。

## 4.2 一机一码
软件采用一机一码机制，一个卡密只能在一台电脑运行、不可多电脑运行。
## 4.3 软件多开
一台电脑仅允许运行一个软件，不支持软件多开。

## 4.4 软件维护
软件由本人独立原创开发，长期维护更新，提供稳定运行。

# 五、软件获取
公众号"**老男孩的平凡之路**"，后台回复"**爬抖音博主**"获取最新版软件安装包。
<img width="1938" height="364" alt="二维码-公众号放底部v2" src="https://github.com/user-attachments/assets/d3da257e-ed8c-4270-baad-b19ec2f3cf62" />

