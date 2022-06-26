#### 5-1.補足1.インストールエラー　Error in the main configuration
##### エラー内容
Error 500. A technical error has occured.  
Error in the main configuration.  

##### エラーログ  
2022-06-21 20:36:24	223.133.253.183	[1024]	Error in main configuration on pluginsPath -- Path given in pluginsPath for the module jacl2db is ignored, since this module is unknown or deactivated	/var/www/lizmap-web-client-3.5.3/lib/jelix/core/jConfigCompiler.class.php	470
	/
array ( )
2022-06-21 20:36:24	223.133.253.183	[7]	Error in the main configuration. A plugin doesn't exist -- The coord plugin jacl2 is unknown.	/var/www/lizmap-web-client-3.5.3/lib/jelix/core/jConfigCompiler.class.php	206

↑　何がおかしいのか　＝　jelix（jacl2db）が気に入らない？　＝　PHP　も怪しい？？？  
↑　それってどういう意味　＝　要するにインストールがうまくいっていない  

##### 対応策
sudo su  
#PHPのアンインストール  
apt-get -y purge 'php*'  
apt -y autoremove  

#PHPの再インストール  
＃PHP8.0にしたい場合（/lizmap-web-client-3.6は対応しているかも2022/06/22時点）  
apt search php8.0-*  
apt-get -y install php8.0-fpm php8.0-cli php8.0-bz2 php8.0-curl php8.0-gd php8.0-intl php8.0-mbstring php8.0-pgsql php8.0-sqlite3 php8.0-xml php8.0-ldap  
#php8.0-json を明示する必要があるよう  
apt-get install libapache2-mod-php8.0  

#PHP7.3にしたい場合（/lizmap-web-client-3.5はこちらが安定しているかも）  
sudo su  
apt search php7.3-*  
apt-get -y install php7.3-fpm php7.3-cli php7.3-bz2 php7.3-curl php7.3-gd php7.3-intl php7.3-mbstring php7.3-pgsql php7.3-sqlite3 php7.3-xml php7.3-ldap  
apt-get install libapache2-mod-php7.3  

#lizmap-web-client　再インストール  
cd /var/www/lizmap-web-client-3.5.3/  
php lizmap/scripts/script.php lizmap~wmts:capabilities montpellier montpellier  
php lizmap/install/installer.php  

#参考
https://github.com/jelix/jelix/issues/314
