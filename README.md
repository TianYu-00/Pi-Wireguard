# Pi-WireguardOptimize

https://github.com/wg-easy/wg-easy

Docker Compose

```
version: "3.8"
services:
  wg-easy:
    environment:
      # ⚠️ Required:
      # Change below values
      - WG_HOST=raspberrypi.local # ⚠️ Wan Ip or Dynamic DNS
      - PASSWORD=foobar123 # ⚠️ Your login password
      - WG_PORT=51820 # Port which needs to be portwarded
      - WG_MTU=1420 # MTU, maximum transmission unit, 1420 is default but i recommend changing this to 1280
      - WG_DEFAULT_DNS=1.1.1.1 # Your DNS. 1.1.1.1 is cloudflare

      # Optional:
      # - WG_DEFAULT_ADDRESS=10.8.0.x
      # - WG_ALLOWED_IPS=192.168.15.0/24, 10.0.1.0/24
      # - WG_PRE_UP=echo "Pre Up" > /etc/wireguard/pre-up.txt
      # - WG_POST_UP=echo "Post Up" > /etc/wireguard/post-up.txt
      # - WG_PRE_DOWN=echo "Pre Down" > /etc/wireguard/pre-down.txt
      # - WG_POST_DOWN=echo "Post Down" > /etc/wireguard/post-down.txt
      
    image: weejewel/wg-easy
    container_name: wg-easy
    volumes:
      - .:/etc/wireguard
    ports:
      - "51820:51820/udp"
      - "51821:51821/tcp"
    restart: unless-stopped
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    sysctls:
      - net.ipv4.ip_forward=1
      - net.ipv4.conf.all.src_valid_mark=1

```

or use one of the wireguard stack templates from here:
https://github.com/novaspirit/pi-hosted

Why i recommend MTU 1280?  
https://keremerkan.net/posts/wireguard-mtu-fixes/
