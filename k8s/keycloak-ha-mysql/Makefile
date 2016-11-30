build:
	docker build -t akvo/keycloak-ha-mysql:2.0.4.Final .

build-no-cache:
	docker build --no-cache -t akvo/keycloak-ha-mysql:2.0.4.Final .

push:
	docker push akvo/keycloak-ha-mysql:2.0.4.Final

mysql-start:
	docker run --rm --name mysql \
		-e MYSQL_DATABASE=keycloak \
		-e MYSQL_USER=keycloak \
		-e MYSQL_PASSWORD=password \
		-e MYSQL_ROOT_PASSWORD=root_password \
		-d mysql:5.7
keycloak-start:
	docker run --rm --name kc-`date +%s` \
		--link mysql:mysql \
	       	-e MYSQL_DATABASE=keycloak \
		-e MYSQL_USERNAME=keycloak \
		-e MYSQL_PASSWORD=password \
		-e GOOGLE_LOCATION="${GOOGLE_LOCATION}" \
		-e GOOGLE_ACCESS_KEY="${GOOGLE_ACCESS_KEY}" \
		-e GOOGLE_ACCESS_KEY_SECRET="${GOOGLE_ACCESS_KEY_SECRET}" \
		akvo/keycloak-ha-mysql

deploy-test:
	kubectl create -f ./deployment.yaml