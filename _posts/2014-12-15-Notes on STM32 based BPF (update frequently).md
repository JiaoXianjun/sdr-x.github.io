---
date: 2014-12-15 12:00:00
layout: post
title: Notes on STM32 based BPF (update frequently)
thread: 2014121523
categories: hw-sw-fw
tags:  STM32 BPF STM32F4DISCOVERY STM32F4-DISCOVERY
---

**0x00** All you need is a discovery board + a mini-usb cable to computer

**0x01** CN3 connected mode: computer -- USB cable -- onboard STLINK -- onboard STM MCU

**0x02** CN3 disconnected mode: computer --USB  cable -- onboard STLINK -- onboard CN2 -- offboard/other STM MCU

**0x03** CN3 disconnected mode is not for offboard USB-STLINK adapter programming discovery board via CN2! This mode turns discovery board to a BIG USB-STLINK adapter for you to develop your own or the third part STM MCU program!

**0x04** [Using the STM32F4DISCOVERY on the Ubuntu 13.04 Command Line](https://www.alexwhittemore.com/stm32f4discovery-on-ubuntu-command-line/)



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

<script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-1542618827905251"
     crossorigin="anonymous"></script>
