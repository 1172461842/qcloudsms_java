

[TOC]
# Overview
@(��Ѷ�ƶ���)[java|maven|sms]

>Ŀǰ��Ѷ�ƶ���Ϊ�ͻ��ṩ���ڶ��ţ����ʶ��ţ�����֪ͨ�������
>���ڶ����ṩ������Ⱥ������ģ��ID��������ģ��IDȺ���Լ����Ż�ִ��ظ���ȡ��
>���ʶ��ſ���ֱ��ʹ�ù��ڵ�������ģ�壬ֻ���滻��Ӧ�Ĺ��������ֻ����롣
>����֪ͨĿǰ֧��������֤���Լ�����֪ͨ���ܡ�
# Getting Start

##׼��
- [ ] ����APPID�Լ�APPKey
>�ڿ�ʼ���̳�֮ǰ������Ҫ�Ȼ�ȡAPPID��APPkey,������δ���룬�뵽https://console.qcloud.com/sms/smslist�����Ӧ�á�Ӧ����ӳɹ����������APPID�Լ�APPKey,ע��APPID����14xxxxx��ͷ��

- [ ] ����ǩ��
 > �·����ű���Я��ǩ��������Ӧ����ģ�� *������������*  �н������롣

- [ ] ����ģ��
 > �·��������ݱ��뾭����ˣ�����Ӧ���� *������������* �н������롣

������������ɿ�ʼ���뿪����
##��װ
qcloudsms���Բ��ö��ַ�ʽ���а�װ�������ṩ�������ŷ������û�ʹ��
###maven
 Ҫʹ��qcloudsms���ܣ���Ҫ��pom.xml�������������
```
<dependency>
  	<groupId>com.github.qcloudsms</groupId>
  	<artifactId>sms</artifactId>
  	<version>0.0.1</version>
</dependency>
```
###sbt
```
libraryDependencies += "com.github.qcloudsms" % "sms" % "0.0.1"
```
###����
����1 �뽫[Դ����	](https://github.com/qcloudsms/qcloudsms_java/tree/master/src)ֱ�����뵽��Ŀ�����С�
����2 ��[JAR��]( http://maven.oa.com/nexus/content/groups/public/com/github/qcloudsms/sms/0.0.1/sms-0.0.1.jar)ֱ�����뵽���Ĺ����С�
`Note`:
����qcloudsms����Ҫʹ�������ĸ�������Ŀ
[org.json](http://central.maven.org/maven2/org/json/json/20170516/json-20170516.jar) , [httpclient](http://central.maven.org/maven2/org/apache/httpcomponents/httpclient/4.5.3/httpclient-4.5.3.jar), [httpcore](http://central.maven.org/maven2/org/apache/httpcomponents/httpcore/4.4.7/httpcore-4.4.7.jar), [httpmine](http://central.maven.org/maven2/org/apache/httpcomponents/httpmime/4.5.3/httpmime-4.5.3.jar)
`���÷���1��2���ַ�������Ҫ�������ĸ�jar�����빤��`��

##�÷�

>�����Խӿ������ʣ����Բ���[API�ĵ�](http://static.javadoc.io/com.github.qcloudsms/sms/0.0.1/index.html?com/github/qcloudsms/package-summary.html)

���ȵ����
```
import com.github.qcloudsms.*;
```
����qcloudsms��֮����Կ�ʼ���Ͷ��š�

###��������
```java
	   try {
			SmsSingleSender sender = new   SmsSingleSender(appid, "replace with key");
			SmsSingleSenderResult result = sender.send(0, "86", "18326693192", "����Ѷ����֤�����1234", "", "123");
			System.out.print(result);
		} catch (Exception e) {
			e.printStackTrace();
		}
```
> `Note`:���跢�͹��ʶ��ţ�ͬ������ʹ�ô˽ӿڣ�ֻ�轫������"86"��д�ɶ�Ӧ������š�
###ָ��ģ��ID��������
```java
	  //�������ģ�� id Ϊ 123��ģ������Ϊ�����Զ��ţ�{1}��{2}��{3}����ѧ��
	  SmsSingleSender sender = new SmsSingleSender(1104620500,"5f03a35d00ee52a224d7ab048186a2c4");
	  ArrayList<String> params = new ArrayList<String>();
	  params.add("ָ��ģ�嵥��");
	  params.add("����");
	  params.add("С��");
	  SmsSingleSenderResult   result = sender.sendWithParam("86", "18326693192", 123, params, "", "", "");
	  System.out.println(result);
```
> `Note:`���۵������Ż���ָ��ģ��ID�������Ŷ���Ҫ�ӿ���̨������ģ�岢��ģ���Ѿ����ͨ�����ſ����·��ɹ������򷵻�ʧ�ܡ�

###Ⱥ��
```
	// ��ʼ��Ⱥ��
	SmsMultiSender multiSender = new SmsMultiSender(appid, "replace with key");
	// ��ͨȺ��
	// ������ 3 ������ĺ���
	ArrayList<String> phoneNumbers = new ArrayList<String>();
	phoneNumbers.add("13101116651");
	phoneNumbers.add("13101116652");
	phoneNumbers.add("13101116653");
	SmsMultiSenderResult multiSenderResult = multiSender.send(0, "86", phoneNumbers, "���Զ��ţ���ͨȺ�������ڣ�С������ѧ��", "", "");
	System.out.println(multiSenderResult);
```
###ָ��ģ��IDȺ��
```
	SmsMultiSender multiSender = new SmsMultiSender(appid, "replace with key");
		// ������ 3 ������ĺ���
	ArrayList<String> phoneNumbers = new ArrayList<String>();
	phoneNumbers.add("13101116651");
	phoneNumbers.add("13101116652");
	phoneNumbers.add("13101116653");
	// �������ģ�� id Ϊ 123��ģ������Ϊ�����Զ��ţ�{1}��{2}��{3}����ѧ��
	params = new ArrayList<String>();
	params.add("ָ��ģ��Ⱥ��");
	params.add("����");
	params.add("С��");
	multiSenderResult = multiSender.sendWithParam("86", phoneNumbers, 123, params, "", "", "");
	System.out.println(multiSenderResult);
```
> `Note:`Ⱥ��һ���������֧��200�����룬���жԺ���������������������ϵ��Ѷ�ƶ��ż���֧��(QQ:3012203387)��

###����������֤��
```java
    //������֤�뷢��
	   SmsVoiceVerifyCodeSender smsVoiceVerifyCodeSender = new SmsVoiceVerifyCodeSender(appid,appkey);
	   SmsVoiceVerifyCodeSenderResult smsVoiceVerifyCodeSenderResult = smsVoiceVerifyCodeSender.send("86","1310555552", "123",2,"");
	   System.out.println(smsVoiceVerifyCodeSenderResult);
```
>`Note`:������֤�뷢��ֻ���ṩ��֤�����֣�������msg=��123��,���յ�������֪ͨΪ������������֤����1 2 3���������Զ������ݣ�����ʹ������֪ͨ

###��������֪ͨ
```
     SmsVoicePromptSender smsVoicePromtSender = new SmsVoicePromptSender(appid, appkey);
     SmsVoicePromptSenderResult smsSingleVoiceSenderResult = smsVoicePromtSender.send("86", "13758028086", 2,2,"��ӭʹ��XXX�����λxxx", "");
	 System.out.println(smsSingleVoiceSenderResult);
```

###��ȡ���Ż�ִ�Լ��ظ�
```
   	SmsStatusPuller pullstatus = new SmsStatusPuller(appid, appkey);
    SmsStatusPullCallbackResult callbackResult = pullstatus.pullCallback(10);
    System.out.println(callbackResult);
    SmsStatusPullReplyResult replyResult = pullstatus.pullReply(10);
    System.out.println(replyResult);
```
> `Note:` ������ȡ������Ҫ��ϵ��Ѷ�ƶ��ż���֧��(QQ:3012203387)������ͻ�����ʹ�ô˹���������ȡ�������ͻ�������ʹ�á�

###���͹��ʶ���
���ʶ��Ųο���������


