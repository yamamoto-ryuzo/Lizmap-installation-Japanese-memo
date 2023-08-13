#### 5-1-1.インストールエラー　Error in the main configuration
---
#### エラー内容
Error 500. A technical error has occured.  
Error in the main configuration.  

#### エラーログ  

2022-06-21 20:36:24	223.133.253.183	[1024]	Error in main configuration on pluginsPath -- Path given in pluginsPath for the module jacl2db is ignored, since this module is unknown or deactivated	/var/www/lizmap-web-client-3.5.3/lib/jelix/core/jConfigCompiler.class.php	470
	/
array ( )
2022-06-21 20:36:24	223.133.253.183	[7]	Error in the main configuration. A plugin doesn't exist -- The coord plugin jacl2 is unknown.	/var/www/lizmap-web-client-3.5.3/lib/jelix/core/jConfigCompiler.class.php	206

↑　何がおかしいのか　＝　jelix（jacl2db）が気に入らない？　＝　PHP　も怪しい？？？  
↑　それってどういう意味　＝　要するにインストールがうまくいっていない  

#### 対応策  まずは古いPHPのアンインストール  
sudo su  
#PHPのアンインストール  
sudo apt-get -y purge 'php*'  
sudo apt -y autoremove  

#### 2022-08-12 /lizmap-web-client-3.6.5　の場合はこちら  
#PHPの再インストール  
＃PHP8.2にしたい場合（/lizmap-web-client-3.6は対応しているかも2022/06/22時点）  
sudo apt -y install php8.2-fpm php8.2-cli php8.2-bz2 php8.2-curl php8.2-gd php8.2-intl php8.2-mbstring php8.2-pgsql php8.2-sqlite3 php8.2-xml php8.2-ldap php8.2-redis  
#php8.2-json を明示する必要があるよう  
apt-get install libapache2-mod-php8.2  

#### 2022-06-21 /lizmap-web-client-3.5　の場合はこちら  
#PHPの再インストール  
#PHP7.3にしたい場合
sudo su  
apt search php7.3-*  
sudo apt-get -y install php7.3-fpm php7.3-cli php7.3-bz2 php7.3-curl php7.3-gd php7.3-intl php7.3-mbstring php7.3-pgsql php7.3-sqlite3 php7.3-xml php7.3-ldap  
sudo apt-get install libapache2-mod-php7.3  

#lizmap-web-client　再インストール  
cd /var/www/lizmap-web-client-3.6.5/  
php lizmap/install/configurator.php  
php lizmap/install/installer.php  

## 参考 ##  
https://github.com/jelix/jelix/issues/314  
