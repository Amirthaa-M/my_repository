import json
import datetime

def transform_data1(data):
    result = []
    for entry in data:
        transformed = {
            "timestamp": entry.get("timestamp"),  
            "temperature": entry.get("temperature"),
            "humidity": entry.get("humidity")
        }
        result.append(transformed)
    return result

def transform_data2(data):
    result = []
    for entry in data:
        iso_time = entry.get("time")  
        if iso_time:
            date = datetime.datetime.strptime(iso_time, '%Y-%m-%dT%H:%M:%S.%fZ')
            timestamp_ms = int((date - datetime.datetime(1970, 1, 1)).total_seconds() * 1000)
        else:
            timestamp_ms = None

        transformed = {
            "timestamp": timestamp_ms,
            "temperature": entry.get("temp"),
            "humidity": entry.get("hum")
        }
        result.append(transformed)
    return result

def main():
    try:
        with open("data-1.json") as f1:
            data1 = json.load(f1)
        with open("data-2.json") as f2:
            data2 = json.load(f2)

        transformed1 = transform_data1(data1)
        transformed2 = transform_data2(data2)

        combined = transformed1 + transformed2

        combined.sort(key=lambda x: x["timestamp"] if x["timestamp"] is not None else 0)

        with open("data-result.json", "w") as out_file:
            json.dump(combined, out_file, indent=4)

        print("Data transformation complete. Output saved in data-result.json")

    except Exception as e:
        print("Error:", e)

if __name__ == "__main__":
    main()
