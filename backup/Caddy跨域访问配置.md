```
域名 {
        header {
                Access-Control-Allow-Origin *
                Access-Control-Allow-Methods "GET, POST, OPTIONS"
                Access-Control-Allow-Headers "Content-Type, Authorization"
                Access-Control-Allow-Credentials true
        }

        # 处理 OPTIONS 预检请求
        @preflight {
                method OPTIONS
        }
        handle @preflight {
                respond "OK" 204
        }

        # 反向代理设置
        reverse_proxy /* tg03:8080 {
                header_up Access-Control-Allow-Origin *
                header_up Access-Control-Allow-Methods "GET, POST, OPTIONS"
                header_up Access-Control-Allow-Headers "Content-Type, Authorization"
                header_up Access-Control-Allow-Credentials true
        }
}
```