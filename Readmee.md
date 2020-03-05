#Web
#cd /home
mkdir site
cd site
mkdir www
cd www
nano index.html

#nano /etc/apache2/sites-enabled/000-default.conf
  ServerAdmin webmaster@sekolah.sch.id
  ServeName sekolah.sch.id
  DocumentRoot /home/site/www
  
#nano /etc/apache2/apache.conf
  <Directory /home/site/www/>

SSH

#cd /etc/ssh
nano sshd_config
  Port 2222
  PermitRootLogin no
 
Uji ssh
#ssh root@localhost-p 2222

Proxy

#nano /etc/squid3/squid.conf

  http_port 3128 transparent
  cache_mem 32 MB
  cache_mgr admin@sekolah.sch.id
  visible_hostname sekolah.sch.id
  
  cache_dir ufs /var/spool/squid3 100 16 256
  
  acl CONNECT method CONNECT
  `
  `
  acl local src 192.168.20.x/x
  acl blokir dstdomain "/etc/squid3/blokdomain"
  http_access deny blokir
  http_access allow local
  
  #http_access deny all (beri tanda pagar)
  
#nano /etc/squid3/blokdomain
Restart Squid3
#squid3 -z

#nano /etc/rc.local

  iptables -t nat -A PREROUTING -p tcp -s 192.168.20.x/x --dport 80 -j REDIRECT --to-port 3128

#sh /etc/rc.local
#iptables -t nat -L
