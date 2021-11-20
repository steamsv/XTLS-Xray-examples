# Shadowsocks AEAD 快速上手

服务端 JSON

```json
{
    "inbounds": [
        {
            "port": 12345,
            "protocol": "shadowsocks",
            "settings": {
                "clients": [
                    {
                        "password": "example_user_1",
                        "method": "aes-128-gcm"
                    },
                    {
                        "password": "example_user_2",
                        "method": "aes-256-gcm"
                    },
                    {
                        "password": "example_user_3",
                        "method": "chacha20-poly1305"
                    }
                ],
                "network": "tcp,udp"
            },
            "sniffing": {
                "destOverride": [
                    "http",
                    "tls"
                ],
                "enabled": true
            }
        } 
        
    ],
    "outbounds": [
        {
            "protocol": "freedom"
        },
        {
            "tag": "stream",
            "sendThrough": "0.0.0.0",
            "protocol": "socks",
            "settings": {
                "servers": [
                    {
                        "address": "hk1.dnsunlock.com",
                        "port": 8443,
                        "users": []
                    }
                ]
            }
        }
    ],
    "routing": {
        "domainStrategy": "AsIs",
        "rules": [
            {
                "type": "field",
                "domains": [
                    "geosite:netflix"
                ],
                "outboundTag": "stream"
            }
        ]
    }
}
```

客户端 JSON

```json
{
    "inbounds": [
        {
            "port": 10801,
            "protocol": "socks",
            "settings": {
                "udp": true
            },
            "sniffing": {
                "destOverride": [
                    "http",
                    "tls"
                ],
                "enabled": true
            }
        },
        {
            "port": 10802,
            "protocol": "http",
            "sniffing": {
                "destOverride": [
                    "http",
                    "tls"
                ],
                "enabled": true
            }
        }
    ],
    "outbounds": [
        {
            "protocol": "shadowsocks",
            "settings": {
                "servers": [
                    {
                        "address": "",
                        "port": 12345,
                        "password": "example_user_1",
                        "method": "aes-128-gcm"
                    }
                ]
            }
        }
    ]
}
```

