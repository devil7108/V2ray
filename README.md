#/bin/bash
bash <(curl -L -s https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh)

systemctl start v2ray.service
systemctl enable v2ray.service
systemctl restart v2ray.service

mkdir /usr/local/bin/v2ray
chmod +777 /usr/local/bin/v2ray
cd /usr/local/bin/v2ray
cat > /etc/v2ray/config.json <<-EOF
"inbound": {
        "listen": "127.0.0.1",
        "port": 5227,
        "protocol": "socks",
        "settings": {
            "auth": "noauth",
            "udp": true,
            "ip": "127.0.0.1"
        }
    },
    "outbound": {
        "protocol": "vmess",
        "settings": {
            "vnext": [
                {
            "address": "2.56.242.xyxyIpiloveyou77",
            "port": 5227, 
            "users": [
              {
                
                "id": "221d95f8-12e2-4276-a899-24hhhhhhhhhsssss",
                "level": 0,
                "alterId": 100
              }
            ]
          }
        ]
      }
    },
    "streamSettings": {
            "network": "tcp",
            "security": true,
            "tlsSettings": {
                "serverName": ""
            }
        }
    },
    "outboundDetour": [
        {
            "protocol": "freedom",
            "settings": {},
            "tag": "direct"
        }
  ],
  "routing": {
    "domainStrategy": "IPOnDemand",
    "rules": [
      {
        "type": "field",
        "domain": [          
         "gc.kis.scr.kaspersky-labs.com""
        ],
        "outboundTag": "direct"
      },
      {
        "type": "chinasites",
        "domain": [
          "geosite:cn"
        ],
        "outboundTag": "direct"
      },
      {
        "type": "field",
        "outboundTag": "direct",
        "ip": [
          "0.0.0.0/8",
                        "10.0.0.0/8",
                        "100.64.0.0/10",
                        "127.0.0.0/8",
                        "169.254.0.0/16",
                        "172.16.0.0/12",
                        "192.0.0.0/24",
                        "192.0.2.0/24",
                        "192.168.0.0/16",
                        "198.18.0.0/15",
                        "198.51.100.0/24",
                        "203.0.113.0/24",
                        "::1/128",
                        "fc00::/7",
                        "fe80::/10"
        ]
      }
    ]
  }
}
