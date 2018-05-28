---
title: "Solved-undefined reference to gzopen64"
excerpt: "Compilation error"
categories:
  - articles
tags:
  - Bioinformatics
---

Today, I tried to install a bioinformatics software called [SomaticSniper](https://github.com/genome/somatic-sniper) under its [instructions](https://github.com/genome/somatic-sniper/blob/master/gmt/install.md) while got stuck at the fourth step.

{% highlight bash %}
mkdir somatic-sniper/build  #succeed
cd somatic-sniper/build #succeed
cmake ../ #succeed
make deps #failed
make -j 
make test 
{% endhighlight %}

The errors are listed below, it seems that zlib is not working well in `bam_import.c` file. Therefore, I modified `bam_import.c` file by replacing the `zlib.h` statement to an absolute path.

{% highlight bash %}

/NAME/src/somatic-sniper/1.0.5.0/build/vendor/samtools/bam_import.c:75: undefined reference to gzopen64
./libbam.a(bam_import.o): In function sam_open:
/NAME/src/somatic-sniper/1.0.5.0/build/vendor/samtools/bam_import.c:502: undefined reference to gzopen64
./libbam.a(bam_import.o): In function sam_header_read2:
/NAME/src/somatic-sniper/1.0.5.0/build/vendor/samtools/bam_import.c:125: undefined reference to gzopen64
collect2: ld returned 1 exit status
make[1]: *** [samtools] Error 1
make[1]: Leaving directory /NAME/src/somatic-sniper/1.0.5.0/build/vendor/samtools
make: *** [all-recur] Error 1
{% endhighlight %}



{% highlight bash %}
$locate zlib.h |head -1 
/usr/include/zlib.h

$vi /NAME/src/somatic-sniper/1.0.5.0/build/vendor/samtools/bam_import.c
replace #include <zlib.h> 
to      #include </usr/include/zlib.h>

{% endhighlight %}
Then, remake deps and everything is ok.


