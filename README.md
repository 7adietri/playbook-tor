# playbook-tor

Ansible playbook for managing Tor relays on Debian-based systems.

Please see the role READMEs for requirements and variables:

* [basics](https://github.com/7adietri/ansible-basics)
* [tor](https://github.com/7adietri/ansible-tor)

The script [update-keys](update-keys) can be used to update and
copy the offline keys.

## Inventory Example

A minimal set of variables for a middle relay:

    basics_autoupdate_origins:
      - o=TorProject,n=${distro_codename}
    tor_instances_middle:
      - name: relay
        nickname: MyCoolRelay
        contact_info: "Foo <foo@example.com>"
        or_ports:
          - 443
          - "[abcd::1:2:3:4]:443"

## Unbound

Hosts in the group `tor_unbound` are configured with a basic [Unbound](https://nlnetlabs.nl/documentation/unbound/)
setup. To use it in Tor, add this to the host configuration:

    tor_nameservers: ["127.0.0.1"]

## Prometheus

Hosts in the group `tor_prometheus` are configured with a Prometheus [node_exporter](https://github.com/prometheus/node_exporter)
running on `localhost:9100`. To expose it as a hidden service, add this to the
host configuration:

    tor_default_hidden_services:
      - name: prometheus
        ports: [9100]

See the [tor](https://github.com/7adietri/ansible-tor) role for information on
client authorization.

## Snowflake Proxy

Hosts in the group `tor_snowflake` are configured as [Snowflake](https://snowflake.torproject.org/)
proxies, using the Go binary.

## License

GPLv3
