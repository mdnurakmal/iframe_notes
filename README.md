# use postman or Advanced REST client to inspect cookie

# replace wordpress.conf in /etc/apache2/sites-enabled

VirtualHost *:80>
    DocumentRoot /srv/www/wordpress
    <Directory /srv/www/wordpress>
        Options FollowSymLinks
        AllowOverride Limit Options FileInfo
        DirectoryIndex index.php
        Require all granted

</Directory>
    <Directory /srv/www/wordpress/wp-content>
        Options FollowSymLinks
        Require all granted

 </Directory>
</VirtualHost>

<VirtualHost *:443>
DocumentRoot /srv/www/wordpress
ServerName www.cdpdemoportal.tk
SSLEngine on
SSLCertificateFile certificate.crt
SSLCertificateKeyFile private.key
SSLCertificateChainFile ca_bundle.crt

Header add MyHeader "Hello Joe. It took %D microseconds for Apache to serve this request."
#Header always edit Set-Cookie (.*) "$1; SameSite=None;Secure"
Header edit Set-Cookie ^(.*)$ $1;Secure;SameSite=None


Header unset X-Frame-Options
Header always unset X-Frame-Options
Header Set Access-Control-Allow-Origin "*"
Header Set Access-Control-Allow-Credentials: true


<Directory /srv/www/wordpress>
        Options Indexes FollowSymLinks
        AllowOverride None
                Require all granted
</Directory>

    <Directory /srv/www/wordpress/wp-content>
        Options FollowSymLinks
        Require all granted

 </Directory>

</VirtualHost>
