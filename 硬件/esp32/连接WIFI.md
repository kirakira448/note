
```cpp
#include <Arduino.h>
#include <WiFi.h>
#include <HTTPClient.h>


const char *ssid = "kkkkkkkk-2G"; // wifi ssid 和其他设备搜索到的名称一致
const char *password = "kahdhe4kaxc35d"; // wifi password

void WiFi_Connect()
{
	WiFi.mode(WIFI_STA);
	WiFi.begin(ssid, password);

	while (WiFi.status() != WL_CONNECTED)
	{
		delay(500);
		Serial.print(".");
	}
}

void setup()
{

	Serial.begin(115200); // open the serial port at 115200 bps;
	delay(100);

	Serial.print("Connecting.. ");

	WiFi_Connect();

	Serial.println("WiFi connected");

	Serial.println("IP address: ");
	Serial.println(WiFi.localIP());
}

void loop()
{

	// custom logic
	// ...
}
```