# DockerizeWebApp
**1. Create a new folder/directory**

root@nazeerul:~# mkdir dockerweb

**2. Change directory to newly created folder**

root@nazeerul:~# cd dockerweb

**Create and edit Dockerfile**

    # Base image of gninx
    FROM nginx:latest
    # Working directory
    #WORKDIR /usr/share/nginx/html
    # Copy files into the folder
    COPY . /usr/share/nginx/html
    # Expose
    EXPOSE 80
    # Run command
    CMD ["nginx","-g","daemon off;"]

    #simple configuration
    #COPY nginx.conf /etc/nginx/nginx.conf

**3. Build dockerfile image and named it webapp**

root@nazeerul:~/dockerweb# docker build -t webapp .

**4. Run the image on 8080 port**

root@nazeerul:~/dockerweb# docker run -d -p 8080:80 webapp

**5. Result:**

**6. index.html created inside dockerweb folder**

    <!DOCTYPE html>
    <html>
    <head>
    <style>
    body {background-color: powderblue;}
    h1   {color: blue;}
    h2   {color: yellow;}
    p    {color: red;}
    </style>
    </head>
    <body>

    <h1>This is a a heading size h1</h1>
    <h2>This is a a heading size h2</h2>
    <p>This is a paragraph.</p>

    </body>
    </html>

**7. Create docker-compose.yml**

    version: '3'
    services:
      web:
        build:
          context: .
          dockerfile: Dockerfile

        ports:
          - 8000:80

        volumes:
          #- ./usr/share/nginx/html
          - -v /var/lib/docker/volumes/vol_app/_data

        deploy:
          resources:
            limits:
              cpus: '0.5'
              memory: '128M'
    # if mongodb
    # environnment variable
    # ENV MONGO_DB_USERNAME = admin\
    #     MONGO_DB_PWD=password

**8. Result:**
