# Services - DNS
A collection of nodes has been provisioned to serve as a collection of DNS servers.

- ns1.odin.local (`192.168.1.169`)
- ns2.odin.local (`129.168.1.223`)

## How To
### Add a new name server
To add a new name server, you must first prepare a virtual machine running a linux distro such as Ubuntu. Once prepared, install the relevant software;

- BIND (`sudo apt install bind9 dnsutils`)

Once installed you can start configuring the nameserver. The configuration is stored in the `/etc/bind/` directory.

### New DNS Zone
To create a new DNS zone, create a new `.zone` file in the folder `/etc/bind/zones/` with the same name as the apex domain of the zone. Copy the snippet below into the file, replacing `example.com` with your desired domain;

```
$ORIGIN example.com.
$TTL 500
@                       IN      SOA     ns1.odin.local. admin.example.com. 1 604800 86400 2419200 604800
@                       IN      NS      ns1.odin.local.
@                       IN      NS      ns2.odin.local.
ns1.odin.local.         IN      A       192.168.1.169
ns2.odin.local.         IN      A       192.168.1.223
```

Once you have created the zone file, you can add the following entry to `/etc/bind/named.conf.local`;

```
zone "example.com" {
  type master;
  file "/etc/bind/zones/example.com.zone";
};
```

We must now delegate to the new zone file from the parent zone, in the case of `example.com.` that would be `com.`. To do this, add the following lines to the parent zone file, again replacing `example.com` with your domain;

```
example.com             IN      NS      ns1.odin.local.
example.com             IN      NS      ns2.odin.local.
```

Now you can restart the BIND service with the command; `sudo systemctl restart bind9`.

### Enable DNSSEC
You can cryptographically sign a DNS zone using DNSSEC. To do this you will first need to generate some keys using the following commands;

```sh
cd /var/cache/bind

# Create zone signing key
sudo dnssec-keygen -a NSEC3RSASHA1 -b 2048 -n ZONE example.com

# Create key signing key
sudo dnssec-keygen -f KSK -a NSEC3RSASHA1 -b 4096 -n ZONE example.com
```

Each key consists of two files, a public key and a private key. The public keys can be appended directly to your zone file. Once you've appended the keys to the zone file, you can sign it. Type the following commands to sign the file;

```sh
# Generate salt for the signiture
echo head -c 1000 /dev/random | sha1sum | cut -b 1-16

sudo dnssec-signzone -3 <SALT> -K /var/cache/bind/ -A -N INCREMENT -o example.com -t example.com.zone
```

This will create a copy of your zone file which includes the `RRSIG` records. You can now update the `/etc/bind/named.conf.local` file to point to your signed zone file;

```
zone "example.com" {
  type master;
  file "/etc/bind/zones/example.com.zone.signed";
};
```

The signing process will also create a `dsset-example.com.` file which contains `DS` records to be added to the name server for the parent DNS zone, in this case `com.`.

### Update DNS Zone
When you want to update the entries in a zone or add new entries, you can just modify the `.zone` file directly. However you **must** increment the serial number in the `SOA` record before restarting the service.

If you have signed the zone with DNSSEC then you will need to resign the zone to complete the update;

```sh
sudo dnssec-signzone -3 <SALT> -u -K /var/cache/bind/ -A -N INCREMENT -o example.com -t example.com.zone
sudo systemctl restart bind9
```