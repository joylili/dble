From centos:centos7
RUN yum install -y wget java mysql python3 python3-devel pip3 mysql-devel gcc && \
    yum clean all && rm -rf /var/cache/yum/*

RUN version=$(curl "https://github.com/actiontech/dble/releases/latest"|awk -F "/" '{print $8}') && \
    wget -P /opt https://github.com/actiontech/dble/releases/download/$version%2Ftag/actiontech-dble-$version.tar.gz && \
    tar zxvf /opt/actiontech-dble-$version.tar.gz -C /opt && \
    rm -f /opt/actiontech-dble-$version.tar.gz && \
    pip3 install mysqlclient -i http://pypi.douban.com/simple --trusted-host pypi.douban.com && \
    pip3 install six -i http://pypi.douban.com/simple --trusted-host pypi.douban.com && \
    pip3 install coloredlogs -i http://pypi.douban.com/simple --trusted-host pypi.douban.com && \
    pip3 install rsa -i http://pypi.douban.com/simple --trusted-host pypi.douban.com

COPY quick-start/*.xml /opt/dble/conf/
COPY quick-start/*.cnf /opt/dble/conf/
COPY quick-start/docker_init_start.sh /opt/dble/bin/
COPY quick-start/start_mgr.sh /opt/dble/bin/
COPY wait-for-it.sh /opt/dble/bin/

RUN chmod 777 /opt/dble/bin/*

VOLUME /opt/dble

CMD ["/opt/dble/bin/docker_init_start.sh"]
