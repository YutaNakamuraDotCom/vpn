FROM centos:8.1.1911
ENV APP_ROOT=${APP_ROOT:-/usr/local}
WORKDIR $APP_ROOT
#必要そうなのインストール
RUN yum -y install gcc make which net-tools ncurses openssl wget &&\
#softetherだうんろーど
wget https://github.com/SoftEtherVPN/SoftEtherVPN_Stable/releases/download/v4.32-9731-beta/softether-vpnserver-v4.32-9731-beta-2020.01.01-linux-x64-64bit.tar.gz &&\
tar -xvf softether-vpnserver* &&\
#実行可能ファイルの生成
cd vpnserver && make  i_read_and_agree_the_license_agreement
#premission setting and startup script
RUN cd vpnserver &&\
chmod 600 * && chmod 700 vpncmd && chmod 700 vpnserver &&\
echo -e '\n\
#!/bin/sh\n\
# chkconfig: 2345 99 01\n\
# description: SoftEther VPN Server\n\
DAEMON=/usr/local/vpnserver/vpnserver\n\
LOCK=/var/lock/subsys/vpnserver\n\
test -x $DAEMON || exit 0\n\
case "$1" in\n\
start)\n\
$DAEMON start\n\
touch $LOCK\n\
;;\n\
stop)\n\
$DAEMON stop\n\
rm $LOCK\n\
;;\n\
restart)\n\
$DAEMON stop\n\
sleep 3\n\
$DAEMON start\n\
;;\n\
*)\n\
echo "Usage: $0 {start|stop|restart}"\n\
exit 1\n\
esac\n\
exit 0\n\
' >> /etc/init.d/vpnserver
CMD ["/usr/local/vpnserver/vpnserver", "execsvc"]