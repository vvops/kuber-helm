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