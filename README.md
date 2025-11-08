🐳 Docker for DevOps Engineers – Full Documentation

Goal: Learn Docker from scratch and document it professionally to show solid understanding for DevOps interviews and team leads.

📘 Table of Contents

What is Docker?

Why DevOps Uses Docker

Key Concepts in Docker

Docker Architecture

Installing Docker

Basic Docker Commands

Docker Images & Containers

Dockerfile Explained

Docker Networking

Docker Volumes (Storage)

Docker Compose

Best Practices for DevOps

Real DevOps Example: Deploying an App with Docker Compose

Interview Questions & Answers

🧩 What is Docker?

Docker هو منصة (Platform) مفتوحة المصدر بتمكنك من بناء، تشغيل، وتوزيع التطبيقات في بيئة معزولة اسمها Containers.

🔹 الـ Container = Application + Dependencies + OS libraries
يعني أي تطبيق بيشتغل بنفس الطريقة في أي بيئة (Local – Test – Production).

⚙️ Why DevOps Uses Docker

Docker بيساعد الـ DevOps Engineer في:

Reason	Description
🧱 Consistency	نفس التطبيق يشتغل في كل بيئة بدون مشاكل “It works on my machine” انتهت!
🚀 Speed	تشغيل التطبيقات بسرعة كبيرة مقارنة بالـ VMs.
🧩 Isolation	كل App معزول عن التاني، فمش بيتعارضوا.
📦 CI/CD Integration	Docker جزء أساسي في Pipelines مع Jenkins/GitHub Actions.
💰 Efficiency	استهلاك موارد أقل من الـ Virtual Machines.
🧠 Key Concepts in Docker
Concept	Meaning
Image	قالب ثابت بيحتوي على الـ App والـ Dependencies.
Container	نسخة شغالة من الـ Image.
Dockerfile	ملف بيشرح Docker إزاي يبني Image.
Registry	مكان لتخزين Images زي Docker Hub.
Volumes	تخزين دائم للبيانات.
Networks	الاتصال بين Containers.
🏗️ Docker Architecture

Docker بيتكون من 3 مكونات رئيسية:

Docker Client
→ الأوامر اللي بتكتبها (docker run, docker build, ...).

Docker Daemon (dockerd)
→ السيرفر اللي بينفذ الأوامر فعليًا.

Docker Registry
→ زي Docker Hub لتخزين وسحب الـ Images.

📉 شكل توضيحي:

+--------------------+
|   Docker Client    |
+--------------------+
           |
           v
+--------------------+
|  Docker Daemon     |
+--------------------+
      /          \
     v            v
 Docker Images   Containers

🧰 Installing Docker
🔹 On Ubuntu:
sudo apt update
sudo apt install docker.io -y
sudo systemctl enable docker
sudo systemctl start docker
docker --version

🔹 On Windows/Mac:

حمل Docker Desktop
.

🧾 Basic Docker Commands
Command	Description
docker version	Check version.
docker images	List local images.
docker ps	List running containers.
docker ps -a	List all containers.
docker pull nginx	Download image.
docker run nginx	Run container from image.
docker stop <id>	Stop container.
docker rm <id>	Remove container.
docker rmi <image>	Remove image.
📦 Docker Images & Containers
Create and Run:
docker run -d -p 8080:80 nginx


🔸 -d: Detached mode
🔸 -p: Port mapping (Host:Container)

Check Logs:
docker logs <container_id>

Enter Container:
docker exec -it <container_id> /bin/bash

🏗️ Dockerfile Explained

Dockerfile هو ملف بيبني الـ Image خطوة بخطوة.

Example:
# Base image
FROM node:18-alpine

# Set working directory
WORKDIR /app

# Copy files
COPY package*.json ./
RUN npm install

COPY . .

# Run app
CMD ["npm", "start"]

# Expose port
EXPOSE 3000

Build Image:
docker build -t mynodeapp .

Run Container:
docker run -d -p 3000:3000 mynodeapp

🌐 Docker Networking

Bridge (default): الاتصال بين Containers داخل نفس الـ host.

Host: يستخدم الـ network الخاص بالـ host.

None: بدون Network.

Custom: Network خاص بتسميه أنت.

docker network create mynet
docker run -d --network=mynet nginx

💾 Docker Volumes (Storage)

Used to store data persistently outside the container.

docker volume create mydata
docker run -v mydata:/data nginx


🔹 Useful for databases like MySQL, MongoDB, etc.

🧩 Docker Compose

Tool بيخليك تدير أكتر من Container كأنهم Application واحد.

Example docker-compose.yml:
version: "3"
services:
  web:
    image: nginx
    ports:
      - "8080:80"
  db:
    image: mongo
    volumes:
      - mydata:/data/db

volumes:
  mydata:

Run:
docker-compose up -d

🧠 Best Practices for DevOps

✅ استخدم .dockerignore عشان تقلل حجم الـ image.
✅ خليك تستخدم multi-stage builds.
✅ خزن الـ credentials في env files مش داخل الـ image.
✅ استخدم official base images.
✅ دايمًا افصل App logic عن Data storage.

🚀 Real DevOps Example: Deploying an App with Docker Compose
Example: Node.js + MongoDB App
version: "3.8"
services:
  app:
    build: .
    ports:
      - "3000:3000"
    depends_on:
      - db

  db:
    image: mongo
    volumes:
      - mongo_data:/data/db

volumes:
  mongo_data:

💬 Interview Questions & Answers
Question	Answer
What’s the difference between Image and Container?	Image = blueprint, Container = running instance.
How is Docker different from a VM?	Containers share the host OS kernel, faster and lighter.
What’s a Dockerfile?	Script defining how to build a Docker image.
What is Docker Compose used for?	Managing multi-container applications.
