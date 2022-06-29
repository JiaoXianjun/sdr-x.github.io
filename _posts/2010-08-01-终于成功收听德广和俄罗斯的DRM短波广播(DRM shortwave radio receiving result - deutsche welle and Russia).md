---
date: 2010-08-01 12:00:00
layout: post
title: 终于成功收听德广和俄罗斯的DRM短波广播(DRM shortwave radio receiving result - deutsche welle and Russia)
thread: 257
categories: radio
tags:  DRM shortwave radio SDR mixer 455kHz-12kHz Mixer SWL Shortwave-Listener
---

(原文刊于被sina关闭的我的sina博客)

终于成功收听德广和俄罗斯的DRM短波广播! 

翻了一下自己之前的博客[DRM接收及matlab实验(DRM shortwave radio receiving experiment)](http://sdr-x.github.io/DRM%E6%8E%A5%E6%94%B6%E5%8F%8Amatlab%E5%AE%9E%E9%AA%8C(DRM%20shortwave%20radio%20receiving%20experiment\)/)，发现竟然是2年前了。 

今天终于听到稳定的DRM广播信号了。短波频段传来了稳定清晰地广播音，真的很强大！DRM可能真有能力救活“几乎已经没人听”的短波广播。 

2年前尝试自己做455kHz-->12kHz的变频器，把乐信RP2100的中频输出变频到12kHz音频范围输进笔记本mic口，软件解调收听DRM广播。当时是啥也没听到。2年里一直惦记，这两天又拿出来当时做的变频器折腾，竟然折腾出来了。成功收听到了俄罗斯在阿穆尔河畔共青城（Komsomolsk Amur）发射的俄语/英语DRM广播（15735kHz），以及德国广播电台(deutsche welle)在斯里兰卡的亭可马里（Trincomalee）发射的DRM信号（17525kHz）。一些经验与大家分享一下： 

# 1. 广播时间

DRM广播信号不是24小时都有的，我整理了一下网上关于DRM播出的时间表，如下： 

北京时间|频率|发射台|目标|语言 
--------|----|------|----|----
0000-2400|1008|湖南台|中国|中文
2200-2357|9610|乌鲁木齐|东亚太平洋|中文 
2100-2157|11810|乌鲁木齐|东亚太平洋|英文 
2300-0157|13790|喀什|欧洲*
0000-0357|17510|喀什|欧洲|英文中文 
1700-2257|17580|喀什|欧洲|英文法文中文 
0900-1300|15735|Komsomolsk|Amur|亚洲|俄语英语 
1200-1230|11700|Tiganesti|中国|中文 
1300-1400|17525|Trincomalee|东亚|英文 

目前收听到的15735kHz俄罗斯共青城的信号即上面的上午9点到中午1点的信号，该信号从俄罗斯向南发射，覆盖中国大部。17525kHz的德广信号是从斯里兰卡向东亚方向发射，也收到了。不过1008kHz的湖南台以及11700kHz的Tiganesti(罗马尼亚的一个地方?)信号没收到。17580kHz的从喀什向欧洲广播的信号也没收到。其他的今晚试试看。 

# 2. 天线

收听俄罗斯和德广时，RP2100只用拉杆天线是不行的，一定要在拉杆天线末端连接上长线天线，天线尽可能高架在窗边。我是在北五环外大概19层楼的第14层朝北的窗户，收音机、天线都在窗台上。北面大概60多米还有一座等高的楼。 
  
# 3. 连接线

我是参照"DRM – Miniature Mixer Unit with crystal option"做的混频器（[http://www.sat-schneider.de](http://www.sat-schneider.de)）。 （那个NE602本振所需要的电感做出来真是够费劲。）。发现它的音频输出线不能太长。我之前一直用了一根大概2米的音频延长线，偶然发现这个延长线不同的收纳和摆放方式对接收影响很大，后来干脆弄了短线，效果变好明显。 不知道是不是602驱动能力不足。
  
# 4. 干扰

所有与220V市电网有关的连接要全断开，包括收音机的，笔记本电脑的。我连220V插座，空调，电视能断的都断电了。笔记本电脑的蓝牙，wifi全关，手机拿远。这才能稳定收听广播。一插220V，立刻被噪声淹没。 
  
# 5. 软件设置

电脑上解调软件使用的开源的Dream软件，它不但能解DRM的OFDM信号，也能解普通的AM、SSB、CW等。解DRM的OFDM信号时，信道估计、同步等算法可以有一些option。个人感觉MCL: Number of Iteration 调成4将会使声音连续性提高很多。 
  
# 6. 带宽设置

RP2100的中频一定要打到宽带，窄带的话不足以让带宽10kHz的OFDM信号完全通过。 
  
不过不得不承认，短波还是能明显看到受传播影响比较大，SNR起伏仍然是有的，而且有时也会跌落到解调门限以下。不过总的说来比起传统短波感觉还是好很多，解调门限变低还是明显提高了抗信号起伏的能力，还有就是是没有噪音：只要能解码就基本上没噪音；不能解调即相当于静噪。 
  
第一张图是软件自动显示的电台台标，接收德广时显示deutsche welle，接收俄罗斯广播台时却显示TELEFUNKEN，好像是设备商的名字，汗！ 

![](../media/drm1.jpg)

第二张图是解调的SDC信道星座图以及解调软件显示的一些其他信息。 

![](../media/drm2.jpg)

第三张图是典型的有信号的频谱，最典型特征是OFDM频带边缘和噪底之间非常陡峭。 

![](../media/drm3.jpg)

第4个和第5个附件是德广和俄罗斯广播的解调输出录音（改天仔细听听内容确认一下）。 

[德广录音](../media/drm1.wav)

[俄广录音](../media/drm2.wav)
  
看来在大陆还是能玩DRM的！

记录一下曾经收到的各DRM广播台的距离：

#### 1. 俄罗斯广播，发射地点俄罗斯Komsomolsk Amur（阿穆尔河畔共青城），1986km

#### 2. 德国广播，发射地点斯里兰卡Trincomalee（亭可马里），4929km

#### 3. 新西兰广播，发射地点新西兰Rangitaiki（朗伊泰基），10637km

#### 4. BBC，发射地点葡萄牙Sines（锡尼什），9729km

#### 5. 俄罗斯广播，发射地点罗马尼亚Tiganesti（特列奥尔曼县），7153km

补充一下我最后用的远距离接收设备的配置（比这个DRM帖子更进一步）： 

#### 1. 用了DE 31有源调谐天线，细心的调整该天线的方位，并且和拉杆天线配合使用。 

#### 2. 本振用了DDS模块，频率，纯度，稳定性得到保障。 

#### 3. 笔记本电脑、有源天线、变频器和DDS都使用电池供电而非电源。 

#### 4. 变频器和笔记本之间的音频连线进一步缩短。 

以上4点每一点都对接收效果有明显影响！ 
  
一些残存的印象： 

新西兰的台印象中老放歌。 

俄罗斯的歌和新闻各半吧。 

BBC新闻多些也有音乐。 

德广最反动，老请各国的人过去说各国的不好。还教大家德语。不过这也看得出来德广节目制作的态度认真。 

播出时段都比较短，大该都是1小时左右。 

<div id="disqus_thread"></div>
<script type="text/javascript">
    /* * * CONFIGURATION VARIABLES: EDIT BEFORE PASTING INTO YOUR WEBPAGE * * */
    var disqus_shortname = 'jiaoxianjun'; // required: replace example with your forum shortname

    /* * * DON'T EDIT BELOW THIS LINE * * */
    (function() {
        var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
        dsq.src = '//' + disqus_shortname + '.disqus.com/embed.js';
        (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
    })();
</script>
<noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>


<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-01GGQ8JZW7"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-01GGQ8JZW7');
</script>
