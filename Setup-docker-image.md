Goto v2/ for build initial server CS1.6
```sh
$ docker build -t cs1.6ds:v2 -f v2/Dockerfile v2/
```

After build `cs1.6ds:v2`, setup one by one those commands.
Currently, use metamod version: 1.20, amxmod: 1.8.2
```
# Workaround for "app_update 90" bug, see https://forums.alliedmods.net/showthread.php?p=2518786
/opt/steam/steamcmd.sh +login anonymous  +force_install_dir /opt/hlds +app_update 90 validate +quit
/opt/steam/steamcmd.sh +login anonymous  +force_install_dir /opt/hlds +app_update 70 validate +quit || :
/opt/steam/steamcmd.sh +login anonymous  +force_install_dir /opt/hlds +app_update 10 validate +quit || :
/opt/steam/steamcmd.sh +login anonymous  +force_install_dir /opt/hlds +app_update 90 validate +quit
mkdir -p ~/.steam && ln -s /opt/hlds ~/.steam/sdk32
ln -s /opt/steam/ /opt/hlds/steamcmd
cp files/steam_appid.txt /opt/hlds/steam_appid.txt
cp hlds_run.sh /bin/hlds_run.sh
chmod +x /bin/hlds_run.sh

# cp default config
cp files/server.cfg /opt/hlds/cstrike/server.cfg

# cp maps
cp maps/* /opt/hlds/cstrike/maps/
cp files/mapcycle.txt /opt/hlds/cstrike/mapcycle.txt

# Install metamod
mkdir -p /opt/hlds/cstrike/cpons/metamod/dlls
curl -sqL "http://prdownloads.sourceforge.net/metamod/metamod-1.20-linux.tar.gz?download" | tar -C /opt/hlds/cstrike/cpons/metamod/dlls -zxvf -
cp files/liblist.gam /opt/hlds/cstrike/liblist.gam
# Remove this line if you aren't going to install/use amxmodx and dproto
cp files/plugins.ini /opt/hlds/cstrike/cpons/metamod/plugins.ini

# Install dproto
mkdir -p /opt/hlds/cstrike/cpons/dproto
cp files/dproto_i386.so /opt/hlds/cstrike/cpons/dproto/dproto_i386.so
cp files/dproto.cfg /opt/hlds/cstrike/dproto.cfg

# Install AMX mod X
curl -sqL "http://www.amxmodx.org/release/amxmodx-1.8.2-base-linux.tar.gz" | tar -C /opt/hlds/cstrike/ -zxvf -
curl -sqL "http://www.amxmodx.org/release/amxmodx-1.8.2-cstrike-linux.tar.gz" | tar -C /opt/hlds/cstrike/ -zxvf -
cp files/maps.ini /opt/hlds/cstrike/cpons/amxmodx/configs/maps.ini
```

Ok after finished, you had `cs1.6ds:v2`.

# Next is build `cs1.6ds:v3` from directory `v3/`
