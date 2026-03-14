alias::  [[建站]]
---

- ## 建站的步骤
	- 简单来讲就两步:
		- 开发
		  logseq.order-list-type:: number
		- 部署
		  logseq.order-list-type:: number
- ## 开发技术选型
	- Hexo
	  logseq.order-list-type:: number
- ## 部署方案
	- ### 需求
		- 简单来讲就是:
			- 一个托管网站的地方
			  logseq.order-list-type:: number
			- 一个域名
			  logseq.order-list-type:: number
			- 便宜的 SSL
			  logseq.order-list-type:: number
			- 国内能访问
			  logseq.order-list-type:: number
	- ### Vercel 托管 + 阿里云域名 + Vercel 自动免费 SSL
		- 使用 Vercel 托管网站 。
		- 域名可以不备案。
	- ### Vercel 托管 + CloudFlare 域名 + CloudFlare 免费 SSL + CloudFlare CDN 服务
		- 使用 Vercel 托管网站 。
		- 使用 CloudFlare CDN 服务 提升访问速度，如果 Vercel 托管的网站在国内访问不了，也可以通过这个 CDN 解决。
		- 同时，CloudFlare 可以购买域名 (无需备案)，并提供免费 SSL 服务。
	- ### (阿里云服务器 + Nginx) + 阿里云域名 + (阿里云免费短期 SSL + 自动替换证书脚本)
	  id:: 667555ef-8818-472b-9734-ed012aad7964
		- 阿里云提供免费的 SSL 证书，但是只有 3 个月期限，需要写个脚本，在到期前替换证书。
		- 使用 Nginx 托管静态网站。
		- 阿里云域名需要备案。
	- ### (阿里云服务器 + Nginx) + 阿里云域名 + acme.sh 免费 SSL
		- 使用 [acme.sh](https://github.com/acmesh-official/acme.sh) 生成免费 SSL 证书。
		- 使用 Nginx 托管静态网站。
		- 阿里云域名需要备案。
	- ### (阿里云服务器 + Caddy) + 阿里云域名+ Caddy 免费 SSL
		- 如果服务器的 80 和 443 端口都通公网的话，可以使用 Caddy web 服务器，它有免费 SSL .
		- 阿里云域名需要备案。
	-