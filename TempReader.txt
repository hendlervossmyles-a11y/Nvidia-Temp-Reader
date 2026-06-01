import pynvml as reader
import time
import serial

arduino = serial.Serial(port='COM3', baudrate=9600, timeout=.1)
encoding ='utf-8'

def get_gpu_temp():
    try:
        reader.nvmlInit()
        # Handle for the first GPU (Index 0)
        handle = reader.nvmlDeviceGetHandleByIndex(0)


        # Get Name and Temp
        name = reader.nvmlDeviceGetName(handle)
        temp = reader.nvmlDeviceGetTemperature(handle, reader.NVML_TEMPERATURE_GPU)

        reader.nvmlShutdown()
        return name, temp
    except Exception as e:
        return None, f"Error: {e}"

def name_parse(name):
    # Convert bytes to string if necessary, remove brand, and strip whitespace
    name_str = str(name).replace("NVIDIA GeForce", "").strip()
    # Remove any dashes that might exist in the name to avoid confusing the Arduino
    name_str = name_str.replace("-", " ")
    return name_str

def arduino_send(name, temp):
    try:

        payload = f"{name}-{temp}\n"
        arduino.write(payload.encode('utf-8'))
        print(f"Sent: {payload.strip()}")
    except Exception as e:
        print(f"Error: {e}")
if __name__ == "__main__":
    while True:
        gpu_name, temp = get_gpu_temp()

        if gpu_name:
            name_parse(gpu_name)
            print(f"Device: {gpu_name} | Temp: {temp}°C")
        else:
            print(temp)
        arduino_send(name_parse(gpu_name), temp)
        time.sleep(2)