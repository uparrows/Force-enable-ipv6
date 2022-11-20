# Force enable ipv6

magisk模块，用以解决oos12和oos13 wifi ipv6地址丢失的问题

Force enable ipv6 for oos12&oos13。

一加9Pro 升级oos12后,wifi的ipv6地址一段时间后丢失，降级oos11无该问题 ，提交bug无人理会，重启wifi正常获取v6地址，过一段时间继续丢失，该模块强制开启ipv6，试图解决该问题 .

如图：使用模块前，开机后一段时间ipv6地址丢失
![-1](https://user-images.githubusercontent.com/38988286/202887798-257e48db-d15b-4556-8124-ad3c9c472b3d.jpg)
启用模块后，坚持一天没问题：
![0](https://user-images.githubusercontent.com/38988286/202887938-26969307-9f09-442c-93e5-e8f44bd9a007.jpg)

为什么wifi会丢失ipv6地址呢，这里有一个老哥发的贴子说明：
https://community.oneplus.com/thread/1580521
原因是开启wifi的时候，同ipv4一样，会向验证服务器请求/generate_204，然后在正常情况下服务器会返回HTTP 204状态，然后设备就会认为你的ip是通的，然而这些服务器不一定能够正常访问，导致设备认为我们的ipv6连不通，所以关闭v6。

本模块的原理是向/proc/sys/net/ipv6/conf/all/accept_ra /proc/sys/net/ipv6/conf/wlan0/accept_ra /proc/sys/net/ipv6/conf/all/disable_ipv6    /proc/sys/net/ipv6/conf/wlan0/disable_ipv6不断的写入1 0开关，在设备系统写入关闭的开关时，我们反向写入开启的开关，以达到强制开启ipv6的效果。

同样有很多报告ipv6问题的帖子，然而一加选择无视：
https://community.oneplus.com/thread/1546490
https://community.oneplus.com/thread/1086519
https://community.oneplus.com/thread/1345632
https://community.oneplus.com/thread/1452866
不在一一列举
由于未使用过color os ，不知道是否存在同样的问题。
当然，如果你不是经常使用ipv6这对于你无所谓
