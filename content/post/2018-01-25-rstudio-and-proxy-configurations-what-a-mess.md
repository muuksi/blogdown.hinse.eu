---
title: RStudio and proxy configurations - what a mess
author: 'Maximilian Hinse'
date: '2018-01-25'
slug: rstudio-and-proxy-configurations-what-a-mess
categories: [RStudio, helpMePlease]
tags: [rstats, proxy-settings, internet, RStudio]
---

In the last days of work I messed around with Rstudio and my internet connection at my workplace. I waisted a lot of time because I am behind a proxy server.
The internet connection on my MacBook pro with Safari and Firefox worked with autodiscovery of my University's proxy settings. Only in RSTudio I could not get it to work. While trying to install packages, sometimes nothing happend and sometimes a timeout notice occured.
Firing up google, stackoverflow and others resulted in an RStudio support blogpost:  https://support.rstudio.com/hc/en-us/articles/200488488-Configuring-R-to-Use-an-HTTP-Proxy


library(devtools)
install_github("gregce/ipify")
library(ipify)
get_ip()
<img src="/post/2018-01-25-rstudio-and-proxy-configurations-what-a-mess_files/sunny side of the pyramid pie-1.png" alt="The sunny side of the pie" width="100%" height="100%"/>


```{r}
# https://support.rstudio.com/hc/en-us/articles/200488488-Configuring-R-to-Use-an-HTTP-Proxy
Sys.getenv ('http_proxy')
Sys.setenv(http_proxy = 'http://proxy.charite.de:8080/')
# file.edit('~/.Renviron') #http_proxy=http://proxy.dom.com/
options(internet.info = 1)

devtools::install_github("crsh/citr")

library(httr)

#with_config(use_proxy("http://proxy.charite.de", 8080, auth = "any"), devtools::install_github("crsh/citr"))
set_config(use_proxy("http://proxy.charite.de", 8080, auth = "any"))
install.packages("RefManageR")

# https://support.rstudio.com/hc/en-us/articles/206827897-Secure-Package-Downloads-for-R
getOption("download.file.method")
options(download.file.method = "libcurl")
install.packages("RefManageR")

```

