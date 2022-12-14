NAME: nginx
LAST DEPLOYED: Tue Oct 25 10:24:11 2022
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
CHART NAME: nginx-ingress-controller
CHART VERSION: 9.3.18
APP VERSION: 1.4.0

** Please be patient while the chart is being deployed **

The nginx-ingress controller has been installed.

Get the application URL by running these commands:

 NOTE: It may take a few minutes for the LoadBalancer IP to be available.
        You can watch its status by running 'kubectl get --namespace default svc -w nginx-nginx-ingress-controller'

    export SERVICE_IP=$(kubectl get svc --namespace default nginx-nginx-ingress-controller -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
    echo "Visit http://${SERVICE_IP} to access your application via HTTP."
    echo "Visit https://${SERVICE_IP} to access your application via HTTPS."

An example Ingress that makes use of the controller:

  apiVersion: networking.k8s.io/v1
  kind: Ingress
  metadata:
    name: example
    namespace: default
  spec:
    ingressClassName: nginx
    rules:
      - host: www.example.com
        http:
          paths:
            - backend:
                service:
                  name: example-service
                  port:
                    number: 80
              path: /
              pathType: Prefix
    # This section is only required if TLS is to be enabled for the Ingress
    tls:
        - hosts:
            - www.example.com
          secretName: example-tls

If TLS is enabled for the Ingress, a Secret containing the certificate and key must also be provided:

  apiVersion: v1
  kind: Secret
  metadata:
    name: example-tls
    namespace: default
  data:
    tls.crt: <base64 encoded cert>
    tls.key: <base64 encoded key>
  type: kubernetes.io/tls
