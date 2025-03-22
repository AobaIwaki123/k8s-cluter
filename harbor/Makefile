render:
	helm template harbor harbor/harbor -f values.yml -n harbor > rendered.yaml

install:
	helm install harbor harbor/harbor --namespace harbor -f values.yml

uninstall:
	helm uninstall harbor -n harbor
