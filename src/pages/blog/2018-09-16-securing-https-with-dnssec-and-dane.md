---
templateKey: blog-post
title: Securing HTTPS with DNSSEC and DANE
date: 2018-09-16T18:21:40.262Z
description: Got DNSSEC on a domain? Why not secure your HTTPS web servers with DANE!
tags:
  - dnssec; tlsa; dane; https; dns
---
****

****

**Why do this?**

If you have a DNSSEC validated domain, you can get your HTTPS (or any service that uses an SSL certificate) verified through DNS by storing a hash of the certificate in DNS.

**What you'll need:**

* A valid certificate - if you haven't got one **get one** - it's free and needed to support modern web standards such as Progressive Web Apps, HTTP2 and removes the insecure warning in Google Chrome (look at [LetsEncrypt ](https://letsencrypt.org/)or [Cloudflare](https://www.cloudflare.com/) for how to get a free certificate).
* A DNSSEC validated domain - both your registrar and DNS provider need to support this. _Personally I use Cloudflare for DNS and Google Domains as my registrar._

**Getting started:**

Firstly, open up your web browser and go to the website you wish to secure with DANE and download the certificate.

In Google Chrome, this can be done by clicking on the padlock -> Certificate ->Details -> Copy to File.

![Certificate for ittom.tips](/img/certificate-export.png)

In the Certificate Export Wizard, select Next and then select **Base-64 encoded X.509 (.CER) _<- this bit is important!_**

![Base-64 certificate export](/img/base-64.png)

Save this file somewhere (such as the desktop) and then go to where you saved the file.

Open this in Notepad (or your text editor of choice) and copy the contents into your clipboard.

Now go to <https://www.huque.com/bin/gen_tlsa> and paste the certificate into the box.

![Enter the options to generate the TLSA record](/img/generate-tlsa-record.png)

Make sure that the radio boxes above the box match my example (3 1 1) and fill in the Port Number, Transport Protocol and Domain Name are filled in correctly. In my example, this is set to port 443 (TCP) for ittom.tips.

Next, click the Generate button and copy the generated DNS record somewhere. Then we need to go to our DNS provider to place the record for which instructions will differ - below are the screenshots for how this is set up on Cloudflare:

![TLSA Record Configuration for ittom.tips](/img/tlsa-record.png)

Generally speaking, the record type should be set to TLSA and should have the name of _443._tcp._subdomain.domain.tld _replacing the subdomain and domain with yours.

Once this is done, we can check if we've set this up correctly by going to <https://www.huque.com/bin/danecheck> and filling in the Domain Name and Port Number.

![Checking the DANE/TLSA record](/img/dane-check.png)

And here are the results:

![The results for ittom.tips](/img/dane-check-results.png)

And that's it! Your certificate is now secured with DNSSEC!
