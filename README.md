Start coredns root/container on RHEL similar Linux

Init repo playbook, raw... -  @work.
2Do - a lot ..

#####
Poll dns packet from hub.docker.com
docker pull coredns/coredns

Start "by hands":
#
/usr/bin/podman run
   -p 10.0.0.1:53:53/tcp
   -p 10.0.0.1:53:53/udp
   -v /etc/coredns:/etc/coredns:ro
   --name coredns
   --read-only
   --cap-drop ALL
   --cap-add NET_BIND_SERVICE
   coredns/coredns:1.7.0 -conf /etc/coredns/Corefile

#
/usr/bin/podman run  \
     -p 10.0.0.100:53:53/udp \
     -p 10.0.0.100:53:53/tcp \
     -v /etc/coredns:/etc/coredns:Z \
     --name coredns
     coredns/coredns -conf /etc/coredns/Corefile

/usr/bin/podman run  -p 10.0.0.111:53:53/udp -p 10.0.0.111:53:53/tcp -v /etc/coredns:/etc/coredns:ro   --name coredns  coredns/coredns -conf /etc/coredns/Corefile


# Misc notes
1. NetworkManager
a.  systemctl restart NetworkManager
b.  nmcli con down enp0s3 && nmcli con up enp0s3
