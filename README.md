# Gemini Chatbot using ESP8266

## Overview
This project is an AI-powered chatbot built using an ESP8266 microcontroller and Google Gemini API. The chatbot allows users to interact with Gemini directly through the Arduino IDE's serial monitor. By sending user queries to the Gemini API, the ESP8266 returns intelligent and context-aware responses, simulating a dynamic chatbot experience.

## Features
- **WiFi Connectivity**: Seamlessly connects to a WiFi network to access the Gemini API.
- **Secure HTTPS Communication**: Ensures secure data transfer using `WiFiClientSecure`.
- **User-Friendly Interface**: Simple interaction through the Arduino IDE serial monitor.
- **Real-Time AI Responses**: Sends user queries to Gemini and fetches responses instantly.
- **Data Cleaning**: Filters out special characters from the response for clean output.

## Technologies Used
- **Microcontroller**: ESP8266 (NodeMCU)
- **API**: Google Gemini API
- **Communication**: HTTPS (secured via `WiFiClientSecure`)
- **Programming Language**: C++ (Arduino IDE)
- **Libraries**:
  - `ESP8266WiFi`
  - `ESP8266HTTPClient`
  - `ArduinoJson`

## Components Required
- ESP8266 (NodeMCU)
- USB Cable for programming
- Arduino IDE (for code upload)

---

## Installation

### Step 1: Clone the Repository
```bash
git clone https://github.com/Archisman09/Gemini-ESP8266-Chatbot.git
```

### Step 2: Install Required Libraries
In the Arduino IDE, go to **Sketch** -> **Include Library** -> **Manage Libraries** and install the following:
- `ESP8266WiFi`
- `ESP8266HTTPClient`
- `ArduinoJson`

### Step 3: Configure WiFi and API Key
Open the `GeminiChatbot.ino` file and replace the placeholders with your credentials:
```cpp
const char* ssid = "Your_WiFi_Name";
const char* password = "Your_WiFi_Password";
const char* Gemini_Token = "Your_Gemini_API_Key";
```

### Step 4: Upload the Code
- Connect the ESP8266 to your computer.
- In Arduino IDE, select the correct board under **Tools** -> **Board** -> **NodeMCU 1.0 (ESP-12E Module)**.
- Choose the correct port and upload the code.

---

## Usage
1. Open the **Arduino IDE Serial Monitor** at 115200 baud rate.
2. Wait for the ESP8266 to connect to the WiFi.
3. When prompted, type your question into the serial monitor.
4. The ESP8266 sends the query to Gemini and displays the response in the serial monitor.

---

## Code Breakdown

### 1. WiFi Connection
```cpp
WiFi.begin(ssid, password);
```
Establishes a connection to the specified WiFi network.

### 2. User Input and Query Submission
```cpp
Serial.println("Ask your Question : ");
```
Waits for the user to input a question, which is then sent to the Gemini API.

### 3. Sending HTTP POST Request
```cpp
http.begin(client, "https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=" + (String)Gemini_Token);
```
Constructs a secure HTTPS request to Gemini API.

### 4. Parsing Response
```cpp
DynamicJsonDocument doc(2048);
deserializeJson(doc, payload);
String Answer = doc["candidates"][0]["content"]["parts"][0]["text"];
```
Parses the API response and extracts the relevant text from the JSON structure.

### 5. Filtering Special Characters
```cpp
for (size_t i = 0; i < Answer.length(); i++) {
    if (isalnum(c) || isspace(c)) {
        filteredAnswer += c;
    }
}
```
Cleans the response to remove unwanted special characters and symbols.

---

## Troubleshooting
- **WiFi Not Connecting**: Ensure SSID and password are correct. Place the ESP8266 closer to the router.
- **No Response from API**: Verify the API key and ensure that Gemini API is enabled in Google Cloud Console.
- **JSON Parsing Errors**: Increase buffer size if the response exceeds `2048` bytes.

---

## Potential Enhancements
- **OLED Display**: Display chatbot responses on a small OLED screen.
- **Web-Based Interface**: Create a web interface hosted on ESP8266 to send queries.
- **Voice Control**: Integrate voice recognition for hands-free interaction.

---

## License
This project is open-source and available under the [MIT License](LICENSE).

---

## Contact
For inquiries or contributions, feel free to reach out:
- **Archisman Kundu**
- 📩 archismankundu04@gmail.com
- 🔗 [GitHub](https://github.com/Archisman09)  
- 🔗 [LinkedIn](https://www.linkedin.com/in/archisman-kundu-020055269/)

