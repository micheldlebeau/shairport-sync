# shairport-sync in Docker on Raspbian 64bit

## Full setup from brand new install

Replace `Downstairs` with the name you want to give to your setup, which will be seen when using Airplay

```
sudo apt update -y && sudo apt upgrade -y
sudo apt-get remove -y docker docker-engine docker.io containerd runc
sudo reboot

curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh # This might error out, just reboot and move on
sudo reboot

sudo docker run \
  -d \
  --device /dev/snd \
  --env AIRPLAY_NAME=Downstairs \
  --name shairport-sync \
  --net host \
  --restart always \
  kourkis/shairport-sync:latest -- -d hw:0 -c PCM 

```

## Network considerations

If your raspberry pi is running on a different network as your devices, you will need to ensure that your devices can reach the pi, and that the pi can reach your devices on these ports:
- 123/udp
- 6001-6010/udp


## Build the docker image
```bash
./build
```

## Run shairport-sync
```bash
./run
```

The analog audio port is used.

See also [man shairport-sync] for other options.

---

[man shairport-sync]: http://htmlpreview.github.io/?https://github.com/mikebrady/shairport-sync/blob/master/man/shairport-sync.html

