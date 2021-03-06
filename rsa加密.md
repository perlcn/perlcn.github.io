#RSA 加密算法
## 为什么要写这个文章？
今天群里huihui用把原先的js引擎JE执行的RSA算法，用Perl改写了。
而我对RSA一直很感兴趣。

## 了解[RSA的历史](http://localhost-8080.com/2013/12/history-of-rsa/)
了解历史，能够让我们更聪明。
RSA 是由三个提出者 Ron Rivest、Adi Shamir 和 Leonard Adleman 的姓氏首字母组成的。这三个人风格迥异，组成了一个技能互补的完美团队。

## [实例解析RSA机密算法](http://www.cfca.com.cn/zhishi/wz-012.htm)
* ###RSA的原理
RSA的安全基于大数分解的难度。其公钥和私钥是一对大素数（100到200位十进制数或更大）的函数。从一个公钥和密文恢复出明文的难度，等价于分解两个大素数之积（这是公认的数学难题）。

* ###RSA的参数
==p q e d n==
公钥由n和e组成。
p和q 是两个素数。
n=p*q
e与（p-1）*（q-1）乘积互为质数



	互质数的概念：公约数只有1的两个数，他们的关系是互质数。


私钥由d和n组成
$$$d\equiv \frac{mod((p-1)*(q-1)}{e}$$$
等价于
$$$ d*e\ mod\ (p-1)*(q-1) == 1 $$$

* ###加密与加密过程
明文：M
密文：C

	加密： $$$ C\equiv M^e\ mod\ n $$$
    解密： $$$ M\equiv C^d\ mod\ n $$$


## 案例模拟

1  设计公钥密钥
取2个素数p q
比如p=3，q=11.
n=p*q=33
e于2x10=20互为质数，
e 可以=3,7,9,11,13,17,19,21...
这里我们取e=3.
d=7的时候，e*7 mod (p-1)(q-1)=21 mod 20 ==1

这用公钥KU=(e,n)=(3,33);密钥KR=(d,n)=(7,33);


2  信息数字化
自己制定规则将英文，汉字，音频图片等信息转换成数字。
假设明文的数字化：11,05,25

3  加密

```
11对应的密文
C^7 mod 33=11 mod 33=11   =>C=11
05对应的密文
C^7 mod 33=05 mod 33=5    =>C=31
25对应的密文
C^7 mod 33=25 mod 33=25    =>C=16
```


4 解密
```
11对应的明文
M mod 33=11^7 mod 33  =>M=11
31对应的明文
M mod 33=31^7 mod 33  =>M=05
16对应的明文
M mod 33=31^7 mod 33  =>M=25
```

**注意： mod 在本文中有2中含义 同余 和 取余，具体语境具体判断


应用场景1：
主：设计en和dn，dn给客户，客户根据dn，把密文转成明文。
应用场景2：
主：设计en和dn，en给客户，客户根据en，把密码等明文转成密文进行传输。

** e:encrypt  d: decrypt
