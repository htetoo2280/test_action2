-
- ## what is docker compose
- Docker Compose က **multi-container Docker applications** ကို **one command** နဲ့ စတင်၊ ရပ်၊ ပြန်တင်နိုင်စေတဲ့ tool ဖြစ်ပါတယ်။
- သက်ဆိုင်ရာ containers တွေ၊ network, volume settings တွေကို **`docker-compose.yml`** ဖိုင်မှာ သတ်မှတ်ပြီး စနစ်တကျ စီမံနိုင်ပါတယ်။
-
- ## Docker Compose အတွက် အသုံးချမှု
- Development, Testing, Production Environment တို့မှာ **containers ကို အလွယ်တကူ စီမံနိုင်ခြင်း**
- Multiple services (Web server, DB, Cache, Message Queue…) ကို **တစ်ကြိမ်တည်း run** လုပ်နိုင်ခြင်း
- Containers အချင်းချင်း **network ဆက်သွယ်မှု** ကို **auto setup** လုပ်နိုင်ခြင်း
-
- ```checking
  docker compose version
  ```
-
- ```install
  sudo apt install docker-compose
  docker-compose --version
  ```
-
- ## docker-compose.yml ရဲ့ အခြေခံ format
- ```
  version: "3.9"  # compose file version
  services:
    web:
      image: nginx:latest
      ports:
        - "8080:80"
    db:
      image: mysql:8
      environment:
        MYSQL_ROOT_PASSWORD: example
      volumes:
        - db_data:/var/lib/mysql
  
  volumes:
    db_data:
  ```
-
- ## commands
- ```
  # Compose file အရ container တွေကို run
  docker compose up -d
  
  # အားလုံးရပ်
  docker compose down
  
  # logs ကြည့်မယ်
  docker compose logs -f
  
  # အချင်းချင်း container တွေ status
  docker compose ps
  ```
-
- ## checking_compose
- ```
  docker-compose ps
  docker-compose up -d
  docker-compose logs -f
  ```
-
-
- ---------------------
- ## to enter postgres db bash
- ```
  sudo docker exec -it postgres psql -U user -d testdb
  ```
-
- ```
  \l  (db and user list)
  \c testdb (to enter the db)
  \dt (table list)
  \dt *.* (table list detail)
  ```
-
-
-
-
-
-
-