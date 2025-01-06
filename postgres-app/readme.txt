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