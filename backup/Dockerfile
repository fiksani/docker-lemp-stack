FROM phusion/baseimage:latest

RUN \
  rm -rf /etc/service/sshd /etc/my_init.d/00_regen_ssh_host_keys.sh && \
  locale-gen en_US.UTF-8 && \
  export LANG=en_US.UTF-8 && \
  apt-get update && \
  apt-get dist-upgrade -y && \
  apt-get install -y nano wget curl lftp && \
  apt-get clean && \
  apt-get autoremove -y && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Backup data every 12 hours
# Backup the www folder every sunday at 3am
RUN \
    echo "0   */6     * * *    root /opt/backupdatabase.sh  >> /var/log/cron.log 2>&1" >> /etc/cron.d/backups && \

ENV TERM xterm
ADD bin/backupdatabase.sh /opt/backupdatabase.sh
RUN mkdir -p /var/backups && chmod +x /opt/backup*.sh
VOLUME /var/backups

CMD ["/sbin/my_init"]
