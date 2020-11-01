# Issues

## Load Balancing Considerations
To avoid problems when running multiple instances of load balancer, `REGISTRY_HTTP_SECRET` should be set. Secret was generated with `{{ randAlphaNum 12 | b64enc | quote }}` [sprig function](http://masterminds.github.io/sprig/)

Warning from logs:
```
time="2020-10-30T12:41:27.9286658Z" level=warning msg="No HTTP secret provided - generated random secret. This may cause problems with uploads if multiple registries are behind a load-balancer. To provide a shared secret, fill in http .secret in the configuration file or set the REGISTRY_HTTP_SECRET environment variable." go.version=go1.11.2 instance.id=561a3d27-4fce-45ad-a67e-3ce76d6cb9d5 service=registry version=v2.7.1
```

[Documentation](https://docs.docker.com/registry/deploying/#load-balancing-considerations)

## Native basic auth
**Warning:** You cannot use authentication with authentication schemes that send credentials as clear text. You must configure TLS first for authentication to work.

To configure TLS on Ingress level, [automated certificate management](https://kubernetes.github.io/ingress-nginx/user-guide/tls/#automated-certificate-management-with-kube-lego) was used, adding `kubernetes.io/tls-acme: "true"` ingress annotation.

If missing TLS, an error should have been thrown, unfortunatelly this couldn't be done with [sprig fail function](http://masterminds.github.io/sprig/flow_control.html) due to existing bug https://github.com/helm/helm/issues/3026

## 413 Request Entity Too Large
When pushing large layers, the following error will be encountered
```
error parsing HTTP 413 response body: invalid character '<' looking for beginning of value: "<html>\r\n<head><title>413 Request Entity Too Large</title></head>\r\n<body>\r\n<center><h1>413 Request Entity Too Large</h1></center>\r\n<hr><center>nginx/1.19.1</center>\r\n</body>\r\n</html>\r\n"
```

This was solved by adding `nginx.ingress.kubernetes.io/proxy-body-size: "0"` ingress annotation.

## Garbage Collection
For garbage collecttor to run, persistent volume should be mounted on CronJob as well. 