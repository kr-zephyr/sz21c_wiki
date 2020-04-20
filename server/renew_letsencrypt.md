# 정리 중...

### 인증서 갱신
./letsencrypt_auto
// sudo 권한 부여 필요
// 자동으로 패키지 업데이트함
// 이하 로그
scin21c@devscin21c:~/letsencrypt/letsencrypt$ ./letsencrypt-auto
Requesting to rerun ./letsencrypt-auto with root privileges...
[sudo] password for scin21c:
./letsencrypt-auto has insecure permissions!
To learn how to fix them, visit https://community.letsencrypt.org/t/certbot-auto-deployment-best-practices/91979/
Upgrading certbot-auto 1.0.0 to 1.3.0...
Replacing certbot-auto...
Creating virtual environment...
Installing Python packages...
Installation succeeded.
/opt/eff.org/certbot/venv/local/lib/python2.7/site-packages/cryptography/hazmat/primitives/constant_time.py:26: CryptographyDeprecationWarning: Support for your Python version is deprecated. The next version of cryptography will remove support. Please upgrade to a release (2.7.7+) that supports hmac.compare_digest as soon as possible.
  utils.PersistentlyDeprecated2018,
Saving debug log to /var/log/letsencrypt/letsencrypt.log
Plugins selected: Authenticator apache, Installer apache

Which names would you like to activate HTTPS for?
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1: dev.sz21c.com
2: developer.sz21c.com
3: devops.sz21c.com
4: wiki.sz21c.com
5: www.sz21c.com
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Select the appropriate numbers separated by commas and/or spaces, or leave input
blank to select all options shown (Enter 'c' to cancel):
Cert is due for renewal, auto-renewing...
Renewing an existing certificate
Performing the following challenges:
http-01 challenge for dev.sz21c.com
http-01 challenge for developer.sz21c.com
http-01 challenge for devops.sz21c.com
http-01 challenge for wiki.sz21c.com
http-01 challenge for www.sz21c.com
Waiting for verification...
Cleaning up challenges
Deploying Certificate to VirtualHost /etc/apache2/sites-enabled/dev-le-ssl.conf
Deploying Certificate to VirtualHost /etc/apache2/sites-enabled/developer-le-ssl.conf
Deploying Certificate to VirtualHost /etc/apache2/sites-enabled/devops-le-ssl.conf
Deploying Certificate to VirtualHost /etc/apache2/sites-enabled/wiki-le-ssl.conf
Deploying Certificate to VirtualHost /etc/apache2/sites-enabled/www-le-ssl.conf

Please choose whether or not to redirect HTTP traffic to HTTPS, removing HTTP access.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1: No redirect - Make no further changes to the webserver configuration.
2: Redirect - Make all requests redirect to secure HTTPS access. Choose this for
new sites, or if you're confident your site works on HTTPS. You can undo this
change by editing your web server's configuration.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Select the appropriate number [1-2] then [enter] (press 'c' to cancel): 2
Enhancement redirect was already set.
Enhancement redirect was already set.
Enhancement redirect was already set.
Enhancement redirect was already set.
Enhancement redirect was already set.

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Your existing certificate has been successfully renewed, and the new certificate
has been installed.

The new certificate covers the following domains: https://dev.sz21c.com,
https://developer.sz21c.com, https://devops.sz21c.com, https://wiki.sz21c.com,
and https://www.sz21c.com

You should test your configuration at:
https://www.ssllabs.com/ssltest/analyze.html?d=dev.sz21c.com
https://www.ssllabs.com/ssltest/analyze.html?d=developer.sz21c.com
https://www.ssllabs.com/ssltest/analyze.html?d=devops.sz21c.com
https://www.ssllabs.com/ssltest/analyze.html?d=wiki.sz21c.com
https://www.ssllabs.com/ssltest/analyze.html?d=www.sz21c.com
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

IMPORTANT NOTES:
 - Congratulations! Your certificate and chain have been saved at:
   /etc/letsencrypt/live/www.sz21c.com/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/www.sz21c.com/privkey.pem
   Your cert will expire on 2020-07-05. To obtain a new or tweaked
   version of this certificate in the future, simply run
   letsencrypt-auto again with the certonly option. To
   non-interactively renew *all* of your certificates, run
   letsencrypt-auto renew
 - If you like Certbot, please consider supporting our work by:

   Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
   Donating to EFF:                    https://eff.org/donate-le

scin21c@devscin21c:~/letsencrypt/letsencrypt$


### openssl을 이용하여 pem(Privacy-enhanced Electronic Mail) 인증서로터 .p12(private key PKCS#12) 인증서 생성
참고 : https://www.openssl.org 
{% highlight shell %} sudo openssl pkcs12 -export -in /etc/letsencrypt/live/www.sz21c.com/fullchain.pem -inkey /etc/letsencrypt/live/www.sz21c.com/privkey.pem -out keystore.p12 -name tomcat -CAfile /etc/letsencrypt/live/www.sz21c.com/chain.pem -caname root
// 실행 위치에 keystore.p12 파일 생성됨
// 생성 중 keystore.p12를 사용하기 위한 password를 입력해야 한다.
// 이하 로그
scin21c@devscin21c:/home/services$ sudo openssl pkcs12 -export -in /etc/letsencrypt/live/www.sz21c.com/fullchain.pem -inkey /etc/letsencrypt/live/www.sz21c.com/privkey.pem -out keystore.p12 -name tomcat -CAfile /etc/letsencrypt/live/www.sz21c.com/chain.pem -caname root
Enter Export Password:
Verifying - Enter Export Password:
scin21c@devscin21c:/home/services$


### WAS에 적용하기 위해 WAS 재기동

