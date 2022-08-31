# WIFI加密类型

参考：https://bbs.huaweicloud.com/blogs/310197

* 有线等效加密（ WEP ）

有线等效保密（ WEP ）是世界上使用最广泛的 Wi-Fi 安全算法。因为历史的缘故，以及向后兼容的原因，很多路由器的控制面板中，用户会发现该算法位于加密类型选择菜单的首位。后来由于安全性的问题， Wi-Fi 协会于2004年宣布 WEP 正式退役。

* Wi-Fi 访问保护（ WPA ）

该标准于2003年正式启用，正是 WEP 正式退役的前一年。 WPA 设置最普遍的是 WPA-PSK（预共享密钥），而且 WPA 使用了256位密钥，明显强于 WEP 标准中使用的64位和128位密钥。尽管 WPA 较之于 WEP 是有了很大的改善， WPA 标准仍然不够安全。 TKIP 是 WPA 的核心组件，设计初衷是全为对现有 WEP 设备进行固件升级。因此， WPA 必须重复利用 WEP 系统中的某些元素，最终也被黑客利用。

* Wi-Fi 访问保护 II（ WPA2 ）

WPA 标准于2006年正式被 WPA2 取代。 WPA 和 WPA2 之间最显着的变化之一是强制使用 AES 算法和引入 CCMP （计数器模式密码块链消息完整码协议）替代 TKIP。WPA2加密方式是目前使用最广泛的无线加密方式，但仍然不够安全。

* WPA-PSK/WPA2-PSK

WPA和WPA2衍生出来的两种加密方式WPA-PSK和WPA2-PSK，他们之间的区别在于使用的加密算法。WPA-PSK和WPA2-PSK既可以使用TKIP加密算法也可以使用AES加密算法。


# 加密强度
加密强度：WPA2-PSK AES算法  >  WPA-PSK AES算法 > WPA2-PSK TKIP算法 > WPA-PSK TKIP算法 > WEP
