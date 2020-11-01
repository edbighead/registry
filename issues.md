# issues
https://docs.docker.com/registry/deploying/#load-balancing-considerations

time="2020-10-30T12:41:27.9286658Z" level=warning msg="No HTTP secret provided - generated random secret. This may cause problems with uploads if multiple registries are behind a load-balancer. To provide a shared secret, fill in http .secret in the configuration file or set the REGISTRY_HTTP_SECRET environment variable." go.version=go1.11.2 instance.id=561a3d27-4fce-45ad-a67e-3ce76d6cb9d5 service=registry version=v2.7.1

TLS
credentials should be used with TLS only
https://kubernetes.github.io/ingress-nginx/examples/auth/client-certs/#client-certificate-authentication
couldn't use fail due to https://github.com/helm/helm/issues/3026

error parsing HTTP 413 response body: invalid character '<' looking for beginning of value: "<html>\r\n<head><title>413 Request Entity Too Large</title></head>\r\n<body>\r\n<center><h1>413 Request Entity Too Large</h1></center>\r\n<hr><center>nginx/1.19.1</center>\r\n</body>\r\n</html>\r\n"
nginx.ingress.kubernetes.io/proxy-body-size: "0"

for cronjob to run you need to mount the PV as well