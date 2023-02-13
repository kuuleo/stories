# REF https://www.linuxbabe.com/ubuntu/set-up-tegola-vector-tile-server-ubuntu-20-04?utm_source=pocket_reader

## Download Tegola
* [x] Go to the Tegola Github page and download the linux version. You can use the following command to download it in terminal.
`wget https://github.com/go-spatial/tegola/releases/download/v0.15.2/tegola_linux_amd64.zip`
* [x] Unzip it.
```
sudo apt install unzip

unzip tegola_linux_amd64.zip
```

* [x] Move the binary to /usr/local/bin/ directory.
`sudo mv tegola /usr/local/bin/`
