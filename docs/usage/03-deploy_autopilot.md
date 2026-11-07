# Autopilot Deploying Guide


__On Raspberry Pi__

## Autopilot On Duty
```console
uv run ~/BearCar/scripts/drive.py --arch <model_architecture> --model <autopilot_file_name>
```

!!!example
    ```console
    uv run ~/BearCar/scripts/drive.py --arch bearnet --model pilot
    ```

!!!tip
    - The `drive.py` will look for model file in `~/BearCar/models/<model_architecture>` directory.
    - Use argument: `--arch` to specify autopilot model architecture.
    - Use argument: `--model` to specify autopilot model file.
    - Press `Pause` button to start/pause the autopilot.
