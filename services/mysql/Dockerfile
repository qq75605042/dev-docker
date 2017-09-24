FROM mysql:5.7.19

RUN echo Asia/Shanghai > /etc/timezone

ADD ./conf/my.cnf /etc/mysql/conf.d/my.cnf

CMD ["mysqld"]