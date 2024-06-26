---
date: 2014-05-28 19:00:00
layout: post
title: Some efforts and tools on GPS signal replay (GPS重放模拟)
thread: 10245
categories: gps
tags:  HACKRF GPS replay CA-code L5 L1 SDR Software-Defined-Radio hackrf_transfer rtl-sdr rtl2832
---

Some efforts were put on replaying GPS signal, but it is only partially successful, not fully successful. Some tools/scripts, as side products, are useful. Learn many things from here: [http://www.aholme.co.uk/GPS/Main.htm](http://www.aholme.co.uk/GPS/Main.htm)

**WARNING：DO NOT SEND ANY REAL GPS SIGNAL. USE CHAMBER AND CLOSE-LOOP CABLE! MAKE SURE ALL YOUR OPERATIONS ARE LEGAL!**

Get codes, program and sample GPS signals here: [https://github.com/JiaoXianjun/GNSS-GPS-SDR](https://github.com/JiaoXianjun/GNSS-GPS-SDR)

To build the C program "gps_test" in "c" directory (front part of software GPS receiver) after you get the whole repo:

    cd c
    make

To let this make smooth, make sure you have fftw library installed correctly (sudo apt-get install ...). There should be /usr/lib/libfftw.a.

# 1. offline GPS simulation method

## 1.1 use C program "gps_test" to receive GPS signal generated by Matlab script gps_sig_gen.m

**a**. generate GPS signal file by running gps_sig_gen.m in Matlab

        gps_sig_gen.m

to get file gps_sig_tmp.bin

**b**. use "gps_test" program to do some initial demodulation and check C/A codes:

        gps_test gps_sig_tmp.bin 2.046e6 8.184e6 5000

Above program gps_test performs initial GPS signal capture by multi-bins correlation in frequency domain.

gps_sig_tmp.bin: input GPS signal generated by gps_sig_gen.m (MATLAB).

2.046e6: carrier frequency

8.184e6: sampling rate

5000: maximum frequency offset for frequency searching

You will find that C/A codes results are aligned with GPS signal we generate by Matlab script.

## 1.2 use C program "gps_test" to receive GPS signal captured by others instead of my our Matlab script gps_sig_gen.m

        gps_test gps.samples.1bit.I.fs5456.if4092.bin 4.092e6 5.456e6 5000

gps.samples.1bit.I.fs5456.if4092.bin: captured by others and can be downloaded here: [http://www.jks.com/gps/gps.html](http://www.jks.com/gps/gps.html)

You will find C/A codes results are equal to those shown here: [http://www.jks.com/gps/gps.html](http://www.jks.com/gps/gps.html)

# 2. over the air GPS test method

# 2.1 playback gps.samples.1bit.I.fs5456.if4092.bin( [http://www.jks.com/gps/gps.html](http://www.jks.com/gps/gps.html) )

**a**. run gps_bin1bit_log2bin.m in Matlab to generate playback file for HACKRF (they capture GPS signal with 1bit quantization. we convert it to 8bit format which is needed by HACKRF): gps.samples.8bit.IQ.fs5456.baseband.bin

**b**. run gps_Nottingham.grc to playback gps.samples.8bit.IQ.fs5456.baseband.bin over the air. And meanwhile/immediately, 

**c**. use rtl-sdr to capture signal: 

        rtl_sdr -g 60 -f 1575.42e6 -s 2.8e6 -n 19.2e6 rtl_2.8Msps_1575.42MHz.bin

**d**. run proc_rtl_bin_for_gps('rtl_2.8Msps_1575.42MHz.bin') in Matlab to convert 8bit file to 1bit file which is needed by gps_test program：rtl_2.8Msps_1575.42MHz_1bit.bin

**e**. see C/A codes initial capture result by running gps_test program:

        gps_test rtl_2.8Msps_1575.42MHz_1bit.bin 0.62e6 2.8e6 100000

You will find C/A codes results are equal to those shown here: [http://www.jks.com/gps/gps.html](http://www.jks.com/gps/gps.html)

## 2.2 playback gps_sig_tmp_for_hackrf_tx.bin (generated by gps_sig_gen.m) to air by gps.grc.

**a**. run gps.grc to playback gps_sig_tmp_for_hackrf_tx.bin over the air. And meanwhile/immediately, 

**b**. capture air GPS signal by:

        rtl_sdr -g 60 -f 1574.8e6 -s 2.8e6 -n 19.2e6 rtl_2.8Msps_1574.8MHz.bin

**c**. convert captured 8bit file to 1bit bin file which is needed by gps_test: rtl_2.8Msps_1574.8MHz_1bit.bin

        proc_rtl_bin_for_gps('rtl_2.8Msps_1574.8MHz.bin'); (MATLAB)

**d**. RUN: 

        gps_test rtl_2.8Msps_1574.8MHz_1bit.bin 0.62e6 2.8e6 100000

to see GPS signal capture result: C/A codes are supposed to align with our expectation (Matlab script).

**e**. you can also capture air GPS signal with different intermediate frequency by:

        rtl_sdr -g 60 -f 1575.42e6 -s 2.8e6 -n 19.2e6 rtl_2.8Msps_1575.42MHz.bin

**f**. convert captured 8bit file to 1bit bin file which is needed by gps_test: rtl_2.8Msps_1575.42MHz_1bit.bin

        proc_rtl_bin_for_gps('rtl_2.8Msps_1575.42MHz.bin'); (MATLAB)

**g**. RUN: 

        gps_test rtl_2.8Msps_1575.42MHz_1bit.bin 0.62e6 2.8e6 100000
    
to see GPS signal capture result: C/A codes are supposed to align with our expectation (Matlab script).


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
