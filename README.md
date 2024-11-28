#include <IRremote.h>

const int RECV_PIN = 2; // IR receiver pin
IRrecv irrecv(RECV_PIN);
decode_results results;

void setup() {
  Serial.begin(9600);
  irrecv.enableIRIn(); // Start the receiver
  Serial.println("IR Receiver Initialized");
}

void loop() {
  if (irrecv.decode(&results)) {
    Serial.print("Received signal: ");
    Serial.println(results.value, HEX); // Print the received value in HEX format
    irrecv.resume(); // Receive the next value
  } else {
    Serial.println("Waiting for IR signal...");
    delay(1000); // Add a delay to avoid flooding the serial output
  }
}
