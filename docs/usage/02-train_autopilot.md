# Autopilot Training Guide

> __On Raspberry Pi__

## Log in to the Server (Remotely and Securely)

```sh
ssh <username>@<ip_address>
```


!!!example
    ```console
    ssh user@192.168.0.112
    ```

Log in to the server via password (not safe though).

!!!tip
    You can localize yourself by looking at the command prompt displayed in the terminal: `<username>@<hostname>:<current_directory>$`.
    The `<hostname>` part tells you which machine your are logged in (RPi or server).

## Start Training

> __On server__
```console
uv run ~/BearCar/scripts/learn.py --data_dir <data_directory> --arch <model_architecture>
```

!!!example
    ```console
    uv run ~/BearCar/scripts/learn.py --data_dir YYYY-MM-DD-HH-MM --arch bearnet
    ```

Autopilot models will be saved on server at `~/BearCar/data/<data_directory>/models/<model_architecture>/<model_name>.pth`.

## Transfer Model Back to RPi

> __On server__

```console
rsync -av --mkpath --progress <model_file_path> <username>@<rpi_ip>:<bearcar_path>/models/<model_architecture>/<desired_model_name>.pth
```

!!!example
    ```console
    rsync -av --mkpath --progress ~/BearCar/data/YYYY-MM-DD-HH-MM/best_model.pth USERNAME@192.168.0.113:~/BearCar/models/bearnet/pilot.pth
    ```

!!!tip
    You may need to find out the IP address of your Raspberry Pi using command: `ip r`

### Model candidates

There are chances you are not satisfied with the `best_model` picked automatically by the `learn.py`.
To take a peek on all the models, you can list all of them using following commands:

```sh
ls ~/BearCar/data/<data_directory>/models/<model_architecture>/
```

For example,

```console
ep10-mse0.3155.pth  ep2-mse0.3539.pth  ep5-mse0.3169.pth  ep8-mse0.3158.pth
ep11-mse0.3135.pth  ep3-mse0.3436.pth  ep6-mse0.3100.pth  ep9-mse0.3174.pth
ep1-mse0.3611.pth   ep4-mse0.3288.pth  ep7-mse0.3121.pth  learning_curve.png
```

The model files are named as the format: `<epoch_number>-<loss_type><loss_value>.pth`.
The tailing value behind `mse` indicates the performance of the model during the training phase.
Theoretically, The lower the value is the better the model performed.
In this example, `ep6-mse0.3100.pth` was picked as the best model.
You can transfer the second best or any model among these candidates, e.g., `ep5-mse0.3169.pth` to Raspberry Pi.

!!!example
    ```console
    rsync -av --mkpath --progress ~/BearCar/data/YYYY-MM-DD-HH-MM/models/bearnet/ep5-mse0.3169.pth USERNAME@192.168.0.113:~/BearCar/models/bearnet/new_pilot.pth
    ```

### Learning curve

The learning curve is saved as `<bearcar_data_directory>/models/<model_architecture>/learning_curve.png`.
You would like to see a dropping curve instead of a climbing one.

!!!tip
    You can log out of the server by using command: `exit` in the terminal or simply just hit `Ctrl`+`d`.
    Remember to check the computer you are using now.
