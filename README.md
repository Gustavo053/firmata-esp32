# firmata-esp32
A clean firmata with sysex IO commands for ESP-32 boards

The library ConfigurableFirmata includes 04 (four) cases to handle each IO sysex command (digital input, digital output, analog input, pwm output). These cases are in src/FirmataExt.cpp. Another modification is in /src/utility/Boards.h, which includes esp-32 arch definitions (ongoing update work to increase analog inputs)

The file /testesp32/testesp32.ino is a light version for board uploading. All unnecessary lines are due commented.

Tested with Javascript firmata: https://github.com/firmata/firmata.js?utm_source=recordnotfound.com. For iterative use of sysexResponse function (for instance, inside a setInverval block), the exception test-block must be removed (or commented):https://github.com/firmata/firmata.js/blob/master/packages/firmata-io/lib/firmata.js

sysexResponse(commandByte, handler) {
    //comment these lines (2373-2375)
    /*if (Firmata.SYSEX_RESPONSE[commandByte]) {
      throw new Error(`${commandByte} is not an available SYSEX_RESPONSE byte`);
    }*/

   Firmata.SYSEX_RESPONSE[commandByte] = board => handler.call(board, board.buffer.slice(2, -1));

   return this;
  }
  
  firmata.js is the file from https://github.com/firmata/firmata.js/blob/master/packages/firmata-io/lib/firmata.js with this modification.
  
  Tested with Ruby arduino-firmata: https://github.com/shokai/arduino_firmata, also installed by https://rubygems.org/gems/arduino_firmata/versions/0.3.7
  
  Tested with Python pyfirmata: https://pyfirmata.readthedocs.io/en/latest/, also installed by https://pypi.org/project/pyFirmata/
  --------------------
