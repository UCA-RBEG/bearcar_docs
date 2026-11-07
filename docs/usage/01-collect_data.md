# Data Collection Guide

## Engage Human Driver

> __On Raspberry Pi__

```console
cd ~/BearCar/scripts
uv run drive.py
```

!!!tip
    - Press `Pause` button to start/pause BearCar.
    - Press `Record` button to activate/deactivate data recording.
    - Data will be saved to `~/BearCar/data/YYYY-MM-DD-HH-MM/`. `YYYY-MM-DD-HH-MM` is the date and time when you start `drive.py`. For example, `2000-01-02-03-04`
    - A valid data directory contains: `~/BearCar/data/YYYY-MM-DD-HH-MM/images/` directory and `~/BearCar/data/YYYY-MM-DD-HH-MM/labels.csv` file.

## Transfer Data to Computing Server

> __On Raspberry Pi__

You can definitely train an autopilot on the Raspberry Pi, but do so would take **forever**.

!!!success
    It is recommended to transfer the data on the Raspberry Pi to a computation dedicated computer.

```console
rsync -av --progress --partial <data_directory> <username>@<ip_address>:<bearcar_directory>/data/
```

!!!example
    ```console
    rsync -av --progress --partial ~/BearCar/data/YYYY-MM-DD-HH-MM USERNAME@192.168.0.112:~/BearCar/data/
```

!!!tip
    - Replace `YYYY-MM-DD-HH-MM` with actual data directory's name.
    - To find out targeted data directory: `ls ~/BearCar/data`.
    - Replace `USERNAME` with your username on the server.

