1) для доступа в контейнер из вне будет необходимо сделать port forword
"kubectl.exe port-forward pods/deployment-postgres-6868987794-csvnz 5432:5432"
2) создание тестовой таблицы 
CREATE TABLE "Link" (
  "id" SERIAL NOT NULL,
  "url" TEXT NOT NULL,
  "hash" TEXT NOT NULL,

  CONSTRAINT "Link_pkey" PRIMARY KEY ("id")
);
3) kubectl.exe rollout restart deployment deployment-postgres рестрат деплоймента 
4) secret. добавить секрет в кубер.  
kubectl.exe create secret generic pg-secret --from-literal PASSWORD=my_pass
хак дешифровки секрета:
kubectl.exe get  secrets pg-secret --template={{.data.PASSWORD}} | base64 -d 
все секреты в кубере не зашифрованы но закодированы в base64 
5) удалить секрет kubectl.exe delete secret pg-secret
6) закодировать в base64 echo -n demo | base64 (убрать новую строку в конце нужен ключ -n)
7) проверка логов в поде kubectl.exe logs short-api-deployment-68b77f9969-vtzwk
8) доступ в контейнер  
kubectl.exe exec -it short-api-deployment-5bfcb59d66-kksqf -- bash
9) Просмотр в реале списка контейнеров kubectl pod --watch
10) Откат новой установленой версии контейнера 
kubectl.exe rollout history deployment short-api-deployment  проверка ревизий 
kubectl.exe apply -f деплоймента
ОТКАТ НА ПРЕДЫДУЩУЮ ВЕРСИЮ :
список ревизий kubectl rollout history  deployment deploy_name
kubectl.exe rollout undo deployment имя_деплоймента --to-revision=2 (номер ревизии для установки)
11) Стрим работы подов   kubectl get pod --watch
12) kubectl get pods -n name_namespace посмотреть поды определенного неймспейса
13) установить ns по умолчанию
kubectl config set-context --current --namespace=имя неймспейса
14) Вывести список ресурсов 
kubectl api-resources --namepaced=false
15) Создание namespace  kubectl create namespace 
посмотреть поды в определеном  ns  kubectl.exe get pod -n my-space
Удалить деплоймент в определенном ns kubectl delete deployments.apps short-app-deployment -n my-space 