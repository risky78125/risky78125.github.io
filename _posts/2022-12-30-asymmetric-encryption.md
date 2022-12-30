---
layout: post
title: "非对称加密"
categories: ssl
author:
- wuqi
meta: "ssl"
---

## 一. 参考

[博客园-拾荒人](https://www.cnblogs.com/gordon0918/p/5363466.html)

## 二. 生成密钥对

### 1. 帮助命令

```
openssl genrsa -
usage: genrsa [args] [numbits]
 -des            encrypt the generated key with DES in cbc mode
 -des3           encrypt the generated key with DES in ede cbc mode (168 bit key)
 -aes128, -aes192, -aes256
                 encrypt PEM output with cbc aes
 -camellia128, -camellia192, -camellia256
                 encrypt PEM output with cbc camellia
 -out file       output the key to 'file
 -passout arg    output file pass phrase source
 -f4             use F4 (0x10001) for the E value
 -3              use 3 for the E value
```
 
### 2. 私钥 - 实际上是密钥对

```
openssl genrsa -aes256 -out key.pem 2048
```

### 3. 公钥 - 从密钥对中提取公钥

```
openssl rsa -in key.pem -pubout -out pub.pem
```

### 4. 查看

```
openssl rsa -in key.pem -noout -text
openssl rsa -in pub.pem -pubin -noout -text
```

## 三. 公钥加密-私钥解密

### 1. 公钥加密

```
openssl rsautl -encrypt -in plain.txt -inkey pub.pem -pubin -out enc.txt
```

### 2. 私钥解密

```
openssl rsautl -decrypt -in enc.txt -inkey key.pem -out replain.txt
```

## 四. 私钥加密-私钥解密

### 1. 私钥加密

实际上是使用密钥对中的公钥进行加密, 同上

```
openssl rsautl -encrypt -in plain.txt -inkey key.pem -out enc.txt
```

### 2. 私钥解密

```
openssl rsautl -decrypt -in enc.txt -inkey key.pem -out replain.txt
```

## 五. 私钥签名-公钥验证

### 1. 私钥签名

```
openssl rsautl -sign -inkey key.pem -in plain.txt -out enc.txt
```

### 2. 公钥验证

```
openssl rsautl -verify -inkey pub.pem -pubin -in enc.txt -out replain.txt
```

