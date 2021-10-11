FROM python:3.9-slim-buster

# RUN apt-get update && apt-get install -y --no-install-recommends gcc musl-dev libc-dev build-essential libbluetooth-dev libgtk2.0-dev
# RUN apt-get update && apt-get install -y --no-install-recommends musl-dev build-essential libbluetooth-dev libgtk2.0-dev
RUN apt-get update && apt-get install -y --no-install-recommends musl-dev build-essential libbluetooth-dev libglib2.0-dev

# http://bugs.python.org/issue19846
# > At the moment, setting "LANG=C" on a Linux system *fundamentally breaks Python 3*, and that's not OK.
ENV LANG C.UTF-8
RUN pip install bluepy requests paho-mqtt pybluez

COPY LYWSD03MMC.py LYWSD03MMC.py
COPY bluetooth_utils.py bluetooth_utils.py
COPY mqtt.conf mqtt.conf
COPY sensors.ini sensors.ini

#RUN setcap cap_net_raw,cap_net_admin+eip $(eval readlink -f `which python3`)
RUN service dbus start
ENTRYPOINT python3 LYWSD03MMC.py --atc -r -b 100 --skipidentical 50 -deb --devicelistfile sensors.ini --mqttconfigfile mqtt.conf