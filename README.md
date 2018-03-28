## Aliyun SMS SDK for PHP

### 安装

composer require huanqiu/aliyun-dysms-php-sdk

### 使用

```php
require_once __DIR__."/vendor/autoload.php";
use Aliyun\Core\Config as AliyunConfig;
use Aliyun\Core\Profile\DefaultProfile;
use Aliyun\Core\DefaultAcsClient;
use Aliyun\Api\Sms\Request\V20170525\SendSmsRequest;
use Aliyun\Api\Sms\Request\V20170525\SendBatchSmsRequest;
use Aliyun\Api\Sms\Request\V20170525\QuerySendDetailsRequest;

// 阿里云Access Key ID和Access Key Secret 从 https://ak-console.aliyun.com 获取
$appKey = '你的Access Key ID';
$appSecret = '你的Access Key Secret';

// 短信签名 详见：https://dysms.console.aliyun.com/dysms.htm?spm=5176.2020520001.1001.3.psXEEJ#/sign
$signName  = '你的短信签名';

// 短信模板Code https://dysms.console.aliyun.com/dysms.htm?spm=5176.2020520001.1001.3.psXEEJ#/template
$template_code = '你的短信模版CODE';

// 短信中的替换变量json字符串
$json_string_param = '你的短信变量替换字符串';

// 接收短信的手机号码
$phone = '接收短信的手机号码';

// 初始化阿里云config
AliyunConfig::load();
// 初始化用户Profile实例
$profile = DefaultProfile::getProfile("cn-hangzhou", $appKey, $appSecret);
DefaultProfile::addEndpoint("cn-hangzhou", "cn-hangzhou", "Dysmsapi", "dysmsapi.aliyuncs.com");
$acsClient = new DefaultAcsClient($profile);
// 初始化SendSmsRequest实例用于设置发送短信的参数
$request = new SendSmsRequest();
// 必填，设置短信接收号码
$request->setPhoneNumbers($phone);
// 必填，设置签名名称
$request->setSignName($signName);
// 必填，设置模板CODE
$request->setTemplateCode($template_code);

// 发起请求
$acsResponse =  $acsClient->getAcsResponse($request);
```