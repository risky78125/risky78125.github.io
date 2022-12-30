---
layout: post
title: "对称加密"
categories: ssl
author:
- wuqi
meta: "ssl"
---

## 参考链接

[博客园-拾荒人](https://www.cnblogs.com/gordon0918/p/5317701.html)

## 帮助命令

`openssl enc -h`, 输出如下: 

```
usage: enc -ciphername [-AadePp] [-base64] [-bufsize number] [-debug]
    [-in file] [-iv IV] [-K key] [-k password]
    [-kfile file] [-md digest] [-none] [-nopad] [-nosalt]
    [-out file] [-pass arg] [-S salt] [-salt]

 -A                 Process base64 data on one line (requires -a)
 -a                 Perform base64 encoding/decoding (alias -base64)
 -bufsize size      Specify the buffer size to use for I/O
 -d                 Decrypt the input data
 -debug             Print debugging information
 -e                 Encrypt the input data (default)
 -in file           Input file to read from (default stdin)
 -iv IV             IV to use, specified as a hexadecimal string
 -K key             Key to use, specified as a hexadecimal string
 -md digest         Digest to use to create a key from the passphrase
 -none              Use NULL cipher (no encryption or decryption)
 -nopad             Disable standard block padding
 -out file          Output file to write to (default stdout)
 -P                 Print out the salt, key and IV used, then exit
                      (no encryption or decryption is performed)
 -p                 Print out the salt, key and IV used
 -pass source       Password source
 -S salt            Salt to use, specified as a hexadecimal string
 -salt              Use a salt in the key derivation routines (default)
 -v                 Verbose

Valid ciphername values:

 -aes-128-cbc              -aes-128-cfb              -aes-128-cfb1
 -aes-128-cfb8             -aes-128-ctr              -aes-128-ecb
 -aes-128-gcm              -aes-128-ofb              -aes-128-xts
 -aes-192-cbc              -aes-192-cfb              -aes-192-cfb1
 -aes-192-cfb8             -aes-192-ctr              -aes-192-ecb
 -aes-192-gcm              -aes-192-ofb              -aes-256-cbc
 -aes-256-cfb              -aes-256-cfb1             -aes-256-cfb8
 -aes-256-ctr              -aes-256-ecb              -aes-256-gcm
 -aes-256-ofb              -aes-256-xts              -aes128
 -aes192                   -aes256                   -bf
 -bf-cbc                   -bf-cfb                   -bf-ecb
 -bf-ofb                   -blowfish                 -camellia-128-cbc
 -camellia-128-cfb         -camellia-128-cfb1        -camellia-128-cfb8
 -camellia-128-ecb         -camellia-128-ofb         -camellia-192-cbc
 -camellia-192-cfb         -camellia-192-cfb1        -camellia-192-cfb8
 -camellia-192-ecb         -camellia-192-ofb         -camellia-256-cbc
 -camellia-256-cfb         -camellia-256-cfb1        -camellia-256-cfb8
 -camellia-256-ecb         -camellia-256-ofb         -camellia128
 -camellia192              -camellia256              -cast
 -cast-cbc                 -cast5-cbc                -cast5-cfb
 -cast5-ecb                -cast5-ofb                -chacha
 -des                      -des-cbc                  -des-cfb
 -des-cfb1                 -des-cfb8                 -des-ecb
 -des-ede                  -des-ede-cbc              -des-ede-cfb
 -des-ede-ofb              -des-ede3                 -des-ede3-cbc
 -des-ede3-cfb             -des-ede3-cfb1            -des-ede3-cfb8
 -des-ede3-ofb             -des-ofb                  -des3
 -desx                     -desx-cbc                 -gost89
 -gost89-cnt               -gost89-ecb               -id-aes128-GCM
 -id-aes192-GCM            -id-aes256-GCM            -rc2
 -rc2-40-cbc               -rc2-64-cbc               -rc2-cbc
 -rc2-cfb                  -rc2-ecb                  -rc2-ofb
 -rc4                      -rc4-40                   -rc4-hmac-md5
```

可以看到支持的加密算法.

## 基本加密

```
openssl enc -aes-256-cfb -in plain.txt -out enc.txt -pass pass:123456
```

## 基本解密

```
openssl enc -aes-256-cfb -d -in enc.txt -pass pass:123456 -out replain.txt
```

## -p -P 参数

打印加密所使用的`salt, key and IV`.

> `-P`不会做加解密操作, 仅打印.

## -a 参数

加密的输出和解密的输入使用`base64`进行转换

## -pass 参数

指定密码的输入方式

* `-pass pass:123456` 通过命令行指定密码
* `-pass file:passwd.txt` 通过文件加载密码
* `-pass env:passwd` 通过环境变量加载密码
* `-pass stdin` 通过控制台输入指定密码

## -S 指定salt的值
