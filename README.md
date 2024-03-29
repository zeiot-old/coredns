# RPI CoreDNS

* Master: [![pipeline status](https://gitlab.com/zeiot/coredns/badges/master/pipeline.svg)](https://gitlab.com/zeiot/coredns/commits/master)

Docker image of [CoreDNS][] to use on a ARM devices.

Exposes Ports :

* `9053` for DNS
* `8080` for health

Exported volumes : `/etc/coredns` and `/var/log/coredns`.

Configure binfmt-support on the Docker host (works locally or remotely, i.e: using boot2docker):

    $ docker run --rm --privileged multiarch/qemu-user-static:register --reset

Then you can run an armhf image from your x86_64 Docker host :

    $ make run version=1.0

Or build :

    $ make build version=1.0


# Usage

There is a sample configuration file (*Corefile*) which forwards all queries to 8.8.8.8 and logs them to stdout.

* Launch CoreDNS:

        $ docker run --rm=true -p 8053:53 -p 8053:53/udp -p 9153:9153 -v `pwd`:/etc/coredns zeiot/rpi-coredns:006

* Then request the DNS:

        $ dig @x.x.x.x -p 8053 www.google.com

* You could see [prometheus][] metrics on : `http://x.x.x.x:9153/metrics`.


# Supported tags

* [![](https://images.microbadger.com/badges/version/zeiot/coredns.svg)](http://microbadger.com/images/zeiot/coredns "Get your own version badge on microbadger.com")


## License

See [LICENSE](LICENSE) for the complete license.


## Changelog

A [ChangeLog.md](ChangeLog.md) is available.


## Contact

Nicolas Lamirault <nicolas.lamirault@gmail.com>


[CoreDNS]: https://coredns.io/
[Prometheus]: https://prometheus.io/
