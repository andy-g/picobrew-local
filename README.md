# Local Picobrew Server (using docker-compose)

## Get started:
```sh
docker-compose up
```

## Setup & Test DNS resolution
![image](https://user-images.githubusercontent.com/557065/134887687-f2d4c01d-0eff-4cc5-bcc8-7af29b0a2416.png)

On the right pane we can see how picobrew resolves to `137.117.17.70` if we don't specify a DNS server, but when we specify a DNS server of `127.0.0.1` (which points to our DNSMASQ cotainer), it resolves to `127.0.0.1`.

We'll need to update our local DNS to use our local server by default.

![image](https://user-images.githubusercontent.com/557065/134887892-cbe2b6ad-cac1-4939-a9a5-743957d4bfbe.png)

Head into your network preferences and add a DNS entry for 127.0.0.1.

![image](https://user-images.githubusercontent.com/557065/134887952-574bfc13-0fdf-4e6b-ad9b-8289de3cde81.png)

And now we no longer need to specify our DNS server, picobrew.com just resolves to the value we specified in the dnsmasq.conf, and other address still work fine.

### handle requests from elsewhere on your network (such as your picobrew)

This will work fine if request are coming from your mac, but if requests are coming from another machine on your network (such as the picobrew), you'll need to tweak the `dnsmasq.conf` file to point to the IP address of your mac on the network instead of `127.0.0.1`.

Tweak the below line in the `dnsmasq.conf` file, replace `127.0.0.1` with the Network IP address of the machine running the docker containers.
```
address=/picobrew.com/127.0.0.1
```

## Cleaning up

If you bring down you local DNS server, you will no longer be able to resolve any DNS addresses, so go back to your system DNS settings, and remove `127.0.0.1`. That should restore your DNS to the value assigned by your local DHCP server.

## ToDo
I haven't been able to test if the `.gitkeep` files cause issues. They are required to create the folder structure required, but if they cause issues we can probably add a setup script to rather create the files.

