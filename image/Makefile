all: docker-build

PLUGINS:=\
	ansible-plugin/build/libs/ansible-plugin-SNAPSHOT.jar \
	slack-incoming-webhook-plugin/build/libs/slack-incoming-webhook-plugin-1.2.5.jar \
	vault-storage-plugin/build/libs/vault-storage-plugin-1.3.3.jar \
	docker-plugin/build/libs/docker-container-1.4.2-SNAPSHOT.zip

ansible-plugin/build/libs/ansible-plugin-SNAPSHOT.jar:
	cd ansible-plugin && docker run --rm -u gradle -v "$$PWD":/home/gradle/ansible-plugin -w /home/gradle/ansible-plugin gradle ./gradlew clean build

slack-incoming-webhook-plugin/build/libs/slack-incoming-webhook-plugin-1.2.5.jar:
	cd slack-incoming-webhook-plugin && docker run --rm -u gradle -v "$$PWD":/home/gradle/slack-incoming-webhook-plugin -w /home/gradle/slack-incoming-webhook-plugin gradle ./gradlew clean build

vault-storage-plugin/build/libs/vault-storage-plugin-1.3.3.jar:
	cd vault-storage-plugin && docker run --rm -u gradle -v "$$PWD":/home/gradle/vault-storage-plugin -w /home/gradle/vault-storage-plugin gradle ./gradlew clean build

docker-plugin/build/libs/docker-container-1.4.2-SNAPSHOT.zip:
	cd docker-plugin && docker run --rm -u gradle -v "$$PWD":/home/gradle/docker-plugin -w /home/gradle/docker-plugin gradle ./gradlew build

clean:
	rm -rf ansible-plugin/build slack-incoming-webhook-plugin/build vault-storage-plugin/build

docker-build: $(PLUGINS)
	docker build -t rundeck-ansible .