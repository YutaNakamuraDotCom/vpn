FROM centos:8.1.1911
ENV APP_ROOT=${APP_ROOT:-/usr/local}
WORKDIR $APP_ROOT
RUN yum -y install gcc make which net-tools ncurses openssl wget &&\
wget https://github.com/SoftEtherVPN/SoftEtherVPN_Stable/releases/download/v4.32-9731-beta/softether-vpnserver-v4.32-9731-beta-2020.01.01-linux-x64-64bit.tar.gz &&\
tar -xvf softether-vpnserver* &&\
cd vpnserver && make  i_read_and_agree_the_license_agreement &&\
chmod 600 * && chmod 700 vpncmd && chmod 700 vpnserver
CMD ["/usr/local/vpnserver/vpnserver", "execsvc"]