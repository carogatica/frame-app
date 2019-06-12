
k_setup :
	kubectl apply -f mongodb/mongo-statefulset.yaml
	kubectl apply -f mongodb/mongo-service.yaml

	kubectl apply -f strapi/app-deployment.yaml
	kubectl apply -f strapi/app-service.yaml
	kubectl apply -f strapi/app-ingress.yaml 

d_setup:
	sudo docker-compose -f docker-compose.yml -p tp6 up -d

	sudo docker exec -ti tp6_bind9_1 route del default;
	sudo docker exec -ti tp6_bgp_1 route del default;
	sudo docker exec -ti tp6_host1_1 route del default;
	sudo docker exec -ti tp6_bind9_1 route add default gw 200.9.21.34;
	sudo docker exec -ti tp6_host1_1 route add default gw 200.9.20.2;


k_clean:
	kubectl delete -f strapi/app-deployment.yaml
	kubectl delete -f strapi/app-service.yaml
	kubectl delete -f strapi/app-ingress.yaml
	kubectl delete -f mongodb/mongo-service.yaml
	kubectl delete -f mongodb/mongo-statefulset.yaml

d_clean:
	sudo docker-compose -f docker-compose.yml -p tp6 down

gui:
	#microk8s.kubectl proxy --accept-hosts=.* --address=0.0.0.0 &
	google-chrome http://192.198.56.4:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/ &

strapi_own:
	google_chrome https://f.efn.unc.edu.ar/admin &

strapi_other:
	google-chrome https://b.efn.unc.edu.ar/admin &		

.PHONY: k_setup k_clean d_setup d_clean strapi_own strapi_other
