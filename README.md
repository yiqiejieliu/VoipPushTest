# VoipPushTest
voip push 测试代码

1、制作.pem格式证书

1、将之前生成的voip.cer SSL证书双击导入钥匙串
2、打开钥匙串访问，在证书中找到对应voip.cer生成的证书，右键导出并选择.p12格式,这里我们命名为voippush.p12,这里导出需要输入密码(随意输入，别忘记了)。
3、目前我们有两个文件，voip.cer SSL证书和voippush.p12私钥，新建文件夹命名为VoIP、并保存两个文件到VoIP文件夹。
4、把.cer的SSL证书转换为.pem文件，打开终端命令行cd到VoIP文件夹、执行以下命令
openssl x509 -in voip.cer  -inform der -out VoiPCert.pem
5、把.p12私钥转换成.pem文件，执行以下命令（这里需要输入之前导出设置的密码）
openssl pkcs12 -nocerts -out VoIPKey.pem -in voippush.p12
6、再把生成的两个.pem整合到一个.pem文件中
cat VoiPCert.pem VoIPKey.pem > ck.pem
最终生成的ck.pem文件一般就是服务器用来推送的。

2、下载服务端推送代码并修改配置信息

下载后一并放入VoIP文件夹中,并配置好相关信息，注意下面图片中提到的推送环境，请填写对应的环境地址，一般测试VoIP推送的稳定性最好是通过Hoc证书打包在生产环境中测试。
开发环境地址：gateway.sandbox.push.apple.com:2195 
生产环境地址： gateway.push.apple.com:2195

3、推送测试
用终端命令行cd到我们的VoIP文件夹中，输入： php php文件名.php 就可以收到推送了

voip证书不区分开发和正式环境,所以得确定好环境一致 可以用Adhoc证书打包测试 配合本地通知调试
