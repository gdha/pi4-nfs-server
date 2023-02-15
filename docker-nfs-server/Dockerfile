ARG BUILD_FROM=alpine:latest

FROM $BUILD_FROM

RUN apk --update --no-cache --verbose add bash nfs-utils nfs-utils-openrc openrc iproute2 libcap kmod && \
    rm -v /etc/idmapd.conf /etc/exports                                              && \
    rc-update add nfs

# http://wiki.linux-nfs.org/wiki/index.php/Nfsv4_configuration
RUN mkdir -p /var/lib/nfs/rpc_pipefs                                                     && \
    mkdir -p /var/lib/nfs/v4recovery                                                     && \
    mkdir /exports                                                                       && \
    chmod a+rwxt /exports                                                                && \
    rm -rf /var/cache/apk /tmp /sbin/halt /sbin/poweroff /sbin/reboot                    && \
    echo "rpc_pipefs  /var/lib/nfs/rpc_pipefs  rpc_pipefs  defaults  0  0" >> /etc/fstab && \
    echo "nfsd        /proc/fs/nfsd            nfsd        defaults  0  0" >> /etc/fstab

#EXPOSE 2049

COPY ./exports /etc/
COPY ./nfsd.sh /usr/local/bin/nfsd.sh
COPY ./.bashrc /root/.bashrc

# setup entrypoint
COPY ./entrypoint.sh /usr/local/bin
#ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
#ENTRYPOINT ["/bin/bash"]
ENTRYPOINT ["/usr/local/bin/nfsd.sh"]
