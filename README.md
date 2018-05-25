
<p align="center">
    <img src="id-card.svg">
</p>

<p align="center">
    <img src="https://img.shields.io/github/issues/ofcold/identity-card.svg">
    <img src="https://img.shields.io/github/forks/ofcold/identity-card.svg">
    <img src="https://img.shields.io/github/stars/ofcold/identity-card.svg">
    <img src="https://img.shields.io/github/license/ofcold/identity-card.svg">
</p>

一个简单的身份证号码获取用户信息工具
------------------------

>  中国（大陆地区）公民身份证，数据来源于国家标准GB/T 2260-2007 <a href="http://www.stats.gov.cn/tjsj/tjbz/xzqhdm/" target="blank">（中华人民共和国行政区划代码)</a>

<br>
## 安装

```bash

    composer require ofcold/identity-card
```


## 说明
一个基于中华人民共和国公民身份证的组件可以获取用户信息。这个适用于任何php框架，但是只有当php版本>=7.1时才可以。
<br>
<a href="README_en.md">English Documentation</a>

## 使用

#### 验证你的身份证号码
```php

    //  返回false 或 Ofcold\IdentityCard\IdentityCard
    $result = Ofcold\IdentityCard\IdentityCard::make('32010619831029081');

    if ( $result !== false ) {

        return '您的身份证号码不正确';
    }

    print_r($result->toArray());

```

#### 或运行测试文件
```bash
    php test
```


```php

    try {
        $idCard = Ofcold\IdentityCard\IdentityCard::make('142701198003124054');
        //  Use locale, Current supported zh-cn,en
        // $idCard = Ofcold\IdentityCard\IdentityCard::make('142701198003124054', 'zh-cn');
        $area = $idCard->getArea();
        $gender = $idCard->getGender();
        $birthday = $idCard->getBirthday();
        $age = $idCard->getAge();
        $constellation = $idCard->getConstellation();
    }
    catch (\Exception $e)
    {
        $e->getMessage();
    }


```


#### 返回结果:
```json

Array
(
    [area] => 山西省 运城地区 运城市
    [province] => 山西省
    [city] => 运城地区
    [county] => 运城市
    [gender] => 男
    [birthday] => 1980-03-12
    [age] => 38
    [constellation] => 双鱼座
)

```


## Api
- getArea():string `获取地区`
- getConstellation():string `获取星座`
- getAge():int `获取年龄`
- getBirthday(string $foramt = 'Y-m-d'):string `获取生日`
- getGender():string `获取性别`
- getCounty():string|null `获取县城`
- getCity():string|null `获取城市`
- getProvince():string|null `获取省`
- toArray():array `全部信息`
- toJson(int $option):string `全部信息`
