# cBlocks
cBlocks is a tool that empowers non-experts such as designers or electronics beginners to prototype the Internet of Things(IoT). Prototyping early ideas in the context of the Internet of Things is difficult. Building functional prototypes requires
advanced knowledge in technologies like Internet connectivity, sensor hardware and low level programming. At the same time evaluating the user experience of early concepts is extreme valuable because best practices in design are missing for this emerging and rather unexplored design space. With our system we provide a rapid prototyping tool for Internet of Things applications that is tailored to the needs of non-expert users. We encapsulate hardware details and facilitate easy Internet connections. At the same time our system is open source and therefore ready to be used and extended by the DIY community.

The system designs follows the following **design principles**:

- Plug & Play: No configuration, instant feedback.
- Hardware Abstraction: Act on physical instead of electrical values.
- Grow As You Go: Logic can be programmed on various levels of complexity. Users without knowledge in programming can use IFTTT to programm cBlocks. Users with programming experience can read and control cBlocks direclty via MQTT.
- Internet Connectivity: Intuitive pairing mechanism between cBlocks and bridge.
- Open Everything: New sensors or actuators can be added; external IoT products can be connected; built on an open hardware platform.

Anyone with making knowledge in electronics and programming can build their own cBlocks and provide it to the community. Below are two examples of cBlocks we have built. A button sensor (left) and a vibration motor (right). There are no restrictions, e.g. we also build a kitchen scale cBlock. You are only limited by your imagination!

TODO: Bilder

This document is step-by-step workshop to get started with cBlocks. The first part explains how to create a cBlock and set up the infrastructure to get going. The second part describes how the previously built cBlock can be used. As an example, a vibration cBlock is implemented, which is controlled by Google Assistant. 

## Make Them

In this section we will explain how to build a vibration motor cBlock and how to set up the infrastructure to get started.

### Architecture

First of all lets introduce the cBlocks architecture. This will help you in understanding the individual building blocks of the system.

TODO Bild.

#### cBlocks
These are the core building blocks used to sense and control the physical world. E.g. a temperature sensor, a button or a vibration motor.

#### Visualizer
The Visualizer is a web application meant to display sensor data and control cBlock actuators. It reads meta data
from the backend in order to detect which cBlocks are online and it receives current sensor readings via MQTT. The
state of a cBlock is visualized by user interface controls that depend on the data to be visualized or controlled. Furthermore, there is a data mapping feature. This way a user can attach semantic meaning to generic sensor readings; e. g. certain temperature ranges could be mapped to Cold and Hot, which allows for a more natural language.

#### Bridge
In order to connect cBlocks to the Internet we provide the Bridge component, which is currently implemented using a
Raspberry Pi 3. The Bridge communicates with the individual cBlocks via Wi-Fi (IEEE 802.11n). The Bridge allows for
minimal configuration since it offers a pairing mechanism for local cBlocks. Network credentials are exchanged between
the Bridge and cBlocks in order to connect the cBlocks with the network. An [audio protocol](https://github.com/weckbach/AstroMech) has been developed to broadcast the credentials to all nearby cBlocks.

#### Backend
The Backend is responsible for command/response handling, providing meta data about the cBlocks and semantic
mappings of readings and commands. Command/response handling is necessary because the MQTT protocol does not
provide any request/response model off the shelf. For instance, if the Visualizer sends a “turn off” command to the
RGB-LED, the Backend must check if the request has the correct format and respond with a timeout error message if the cBlock does not react timely. The Backend also provides meta data about the specific cBlocks. For example, the Visualizer reads which resources a cBlock provides, as well as which data type and units those resources use, in order to display them correctly. The temperature and humidity sensor for instance, has two numerical resources Temperature and Relative Humidity.

#### MQTT broker
The MQTT broker is used as a message bus, exchanging real-time sensor readings and actuator commands to and from the cBlocks. TThe MQTT Broker provides the means to connect any third-party software to the system, since it is an established standard in the IoT field.

### Make a cBlock 

Now, let's actually make our first cBlock.

#### Hardware

##### cBlocks Board
In order to get started with cblocks we first have to build the board. The cBlocks board is based on the [Adafruit Feather HUZZAH32 Dev Board](https://learn.adafruit.com/adafruit-huzzah32-esp32-feather/overview). It is an excellent dev board because it has a lot of nice features like the battery charger or the USB to serial converter. Since cBlocks need some more functionalites like a mircophone for pairing, a 5V booster, a status LED and some Buttons, we designed a board around the HUZZAH32. It's kind of a breakout of the breakout. You can find the schematics and the layout here (TODO link). Please order the board at your favorite PCB manufacturer. You can also export the parts list via Eagle and order the parts at your favorite store. As a microphone we use the [MEMS microphone](https://www.sparkfun.com/products/9868) from SparkFun. Also don't forget to order the Adafruit Feather HUZZAH32 itself.

#### cBlocks Protoboard
In addition to the cBlock board there is also a cBlocks protoboard. It a shield that is stacked on top of the cBlock board that has some labeled pin outs. It makes prototyping a little easier, so feel free to order that board as well.

#### Vibration Motor Circuit
For the vibration motor cicuit you need the [Vibrating Mini Motor Disc](https://www.adafruit.com/product/1201) and the [Adafruit DRV2605L Haptic Controller Breakout](https://learn.adafruit.com/adafruit-drv2605-haptic-controller-breakout/overview). Feel free to use any other vibration motor. The hook up is straight forward:

| Protoboard        | DRV2605L           |
| ------------- |:-------------:|
| SDA      |SDA|
| SCL     |SCL|
| 3V3 | VIN|
| GND | GND|

Here is a photo of the final hook up:

TODO Photo.

#### Casing (optional)
#### Arduino SDK
### Bridge
#### Hardware
- Speaker
- Casing
- (Button)
#### Raspbian Image Link
### Backend
#### Start
#### Create an entry in the registry
### Visualizer
## Use Them
1. Bridge
2. Pairing
3. Visualizer
4. Turn On
6. Define Mapping
7. IFTTT
