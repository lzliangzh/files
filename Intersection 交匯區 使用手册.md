# Intersection 交匯區 使用手册

1. 在`~/myServer/my-project/docs`下随意编写 Markdown
2. `mkdocs serve -a 10.7.13.228:8080`，然后 `nginx -s reload `，将网站实时构建公开在局域网上。其中，`10.7.13.228:8080`是本机的局域网 IP 和端口号。
3. `mkdocs build`构建网站但不公开在局域网上