## checking docker image and container
- ```
  ## checking image
  sudo docker images
  
  ## checking container
  sudo docker ps -a 
  ```
-
- ## delete old container
- sudo docker rm $(sudo docker ps -a -q)
-
- rm = run ပြီးတန်းဖျက်
- it = interactive , terminal (input ကို docker ထဲရောက်အောင်လုပ်)
- image ရဲ့ -v ~/.config/rclone မှာရှိတဲ့ folder ကို
- container ရဲ့ /root/.config/rclone ကို mount လုပ်
- rclone/rclone = imgae name
- listremotes = docker command
- ```
  sudo docker run --rm -it -v ~/.config/rclone:/root/.config/rclone rclone/rclone listremotes
  ```
-
-
- #rclone_in_a_docker
- #docker_compose
-
-