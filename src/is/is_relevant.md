# is_relevant
### 部分基于公共基础设施PKI及其应用
### 部分基于精通PKI网络安全认证技术与编程实现文档
### 部分基于中国金融集成电路（IC）卡规范部分内容


### 目录结构
### - [0. 信息安全概述](#0-信息安全概述)
### - [1. 公共基础设施PKI及其应用](#1-PKI公钥基础设施)




## 0-信息安全概述
#### * 信息安全
   * 是指信息系统（包括硬件、软件、数据、人、物理环境及其基础设施）受到保护，不受偶然的或者恶意的原因而遭到破坏、更改、泄露，系统连续可靠正常地运行，信息服务不中断，最终实现业务连续性。
* 信息安全主要包括以下五方面的内容，即需保证信息的保密性、真实性、完整性、未授权拷贝和所寄生系统的安全性。
#### * 常用的安全防范措施
  * 网络层：防火墙、安全路由器、入侵检测IDS及防黑客软件。
  * 应用层：基于PKI的数字证书机制
* 信息已成为企业的资源，信息的核心是数据，所以，保护信息、数据的安全其发展趋势将越来越重要。
#### * 电子商务和电子政务的安全需求
  * 网上身份的真实性认证，网上各种角色的身份进行鉴别与识别
  * 网上交易订单信息要保护其私密性
  * 交易支付信息的完整性
  * 交易各方对其交易和支付的不可抵赖性
#### * 密码学理论基础
  * 保密学（Xryptology）是研究信息系统安全保密的科学。它包含两个分支：密码学（Cryptography）和密码分析学（Cryptanalytics）
	   * 密码学是对信息进行编码实现隐蔽信息的一门学问。
	   * 密码分析学是研究分析破译密码的学问。
#### * 密钥体制
  * 单钥体制(对称密钥)
    * 加密密钥和解密密钥相同，或从一个能够推出另一个，成为单钥或对称密钥体制。
  * 双钥体制（非对称密钥）
    * 加密密钥和解密密钥不相同，则从一个难以推出另一个，则称为双钥或非对称密码体制。
#### * 常用密钥
（来源及密钥分析，种类就不叙述了，更详细了解可以搜索上面提到的文章应用）
  * 单钥体制(对称密钥)
    * SM4 DES 
  * 双钥体制(非对称密钥)
    * SM2 RSA

## 1-PKI公钥基础设施
#### * PKI公钥基础设施
  * 公钥基础设施是利用公钥密码算法构建的安全基础设备，提供应用层面的安全服务。公钥基础设施提供了一个框架，可以在这个框架下实施基于加密的安全服务。
  * PKI是一种遵循标准的利用公钥加密技术为网上电子商务、电子政务的开展，提供一整套安全的基础平台。用户利用PKI平台提供的安全服务进行安全通讯。PKI这
种遵循标准的密钥管理平台，能够为所有网络应用透明地提供采用加密和数字签名等密码服务所需要的密钥和证书管理。
#### * 公钥基础设施的内容
 * 认证机构（Certificate Authority）
   * 认证机构是PKI的核心组成部分，是PKI的核心执行机构，一般简称为CA，在业界通常成为认证中心，它是数字证书的签发机构。证书是数字证书、电子证书的简称，是公开密钥体制的一种密钥管理媒介。它是一种权威性的电子文档，形同网络计算环境中的一种身份证，用于证明某一主体的身份，以及其公开密钥的合法性在使用公钥体制的网络环境中，必须向公钥的使用者证明公钥的真实合法性。
 * 证书库
   * CA颁发证书和撤销证书的集中存放的地方。是网上的一种公共信息库，供广大公众进行开放式查询。
 * 证书撤销
   * 证书撤销的原因：
     * 1、用户身份姓名的改变
     * 2、私钥被窃或泄漏
     * 3、用户与其所属企业关系变更
     * 证书撤销的实现方法有两种
     * 1、利用周期性的发布机制（CRL）
     * 2、在线查询机制（OCSP）
 * 密钥备份和恢复</br>
 ![](https://rainron.github.io/JAVA-LINUX-IS/img/is/keybackuprecover.png)
 * 自动更新密钥
     * 一个证书的有效期是有限的
 * 密钥更新
     * 根据证书的安全策略或CPS（证书运作规范）规定，到期之前，需要颁发一个新的公/私密钥的相关证书。
 * 证书更新与证书恢复
     * 证书恢复是保持最初的公钥/私钥对，而密钥证书更新是在证书中产生了一个新的公钥/私钥对。
 * 密钥历史档案
   * 每个用户都会形成多个“旧”证书和至少一个“当前”的证书。这一系列旧证书和相应的私钥就组成了用户密钥和证书的历史档案，简称密钥历史档案
 * 交叉认证
   * 为了在以前没有联系的PKI之间建立信任关系，引入了“交叉认证”的概念。在没有一个同意的全球的PKI环境下，交叉认证是一个可以接受的机制，不同PKI的用户
团体之间必须进行安全通信。
 * 时间戳</br>
  ![](https://rainron.github.io/JAVA-LINUX-IS/img/is/timestamp.png)
 * 客户端软件
   * 自动查询证书“黑名单”（CRL），实现双向身份认证
   * 对传输信息自动加/解密，保证信息的私密性
   * 证书恢复功能
   * 实现证书生命周期的自动管理
   * 多种证书存放方式
* PKI的相关功能</br>
![](https://rainron.github.io/JAVA-LINUX-IS/img/is/pkiAPI.png)
#### * PKI体系结构概述
  * PKI体系结构一般由多种认证机构与各种终端实体组成。
![](https://rainron.github.io/JAVA-LINUX-IS/img/is/pkiSystem.png)
  * PPA（Policy Approval）是一个大PKI的根CA，如一个国家或一个地域性的CA。
  * PCA（Pllicy Certificate Authority）是PAA下设的政策行CA，如行业CA等。
  * CA（Certificate Authority）是指一般操作CA。
  * ORA(Online Registration Authority)即RA，在线工作的申请注册机构最终的证书用户实体EE（End Entity）









#### * 数据加解密/身份认证流程
![](https://rainron.github.io/JAVA-LINUX-IS/img/is/endeypt.png)



