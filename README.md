# docker-sftp-ngrock
Create an SFTP server based on the docker image
Expose it over the internet with ngrock
Connect to it with FileZile or sftp command line 

# docker-compose.yml
```
version: '3.8'
 
services:
  sftp:
    image: atmoz/sftp
    volumes:
      - ./ssh_test_ed25519.pub:/Users/dan/.ssh/id_ed25519.pub:ro
    ports:
      - "2222:22"
    command: dan:sftpuser:::upload
```
# Steps

- Create a ssh key by following this https://docs.acquia.com/acquia-cloud-platform/manage-apps/command-line/ssh/getting-started/generate
- Update in `docker-compose.yml` the path to the key
- Update command: with sftpUser:password:::destinationFolder

# Run
- docker compose up -> creates the image with SFTP server
- ngrok tcp 2222 -> expose the application on sftp only
- sftp -P2222 dan@127.0.0.1 -> connect from terminal same machine(same network)
- From FireMozila use the port and host from ngrock
- Now you should upload and download info on the SFTP
