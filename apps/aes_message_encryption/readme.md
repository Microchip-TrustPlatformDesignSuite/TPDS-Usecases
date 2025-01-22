# ECC608 AES Message Encryption

This application example demonstrates AES encryption being run on Host MCU or MPU while having
the master symmetric key held securely in ECC608 secure element.

## Description

- The master symmetric key is stored in ECC608 and a derived key is generated using KDF command. The parameters used to calculate the derived key are then shared to the Cloud/
remote host so it can calculate the same derived key to perform AES operations.
- Storing the symmetric key in ECC608 ensures that the master key is never exposed.
- The derived key can also be set to expire (ephemeral key) after a set time frame in the software.
- Once the current key expires, the remote host and MCU/MPU system can agree on parameters
and generate a fresh ephemeral key.

![ECC608 AES Message Encryption Transaction Diagram](./Images/td_aes_message_encryption.png)

## Training Video

<a href="https://www.youtube.com/watch?v=TdexOLD33bs" target="_blank">![](https://img.youtube.com/vi/TdexOLD33bs/0.jpg)</a>

# ATECC608 AES Message Encryption Execution

## Prerequisites

- [Trust Platform Design Suite](https://www.microchip.com/en-us/products/security/trust-platform/tpds)
- [MPLAB® X IDE](https://www.microchip.com/en-us/tools-resources/develop/mplab-x-ide#tabs)
- [Cryptoauth Trust Platform Development Kit](https://www.microchip.com/developmenttools/productdetails/DM320118)

## Setting up [Cryptoauth Trust Platform Development Kit](https://www.microchip.com/developmenttools/productdetails/DM320118)

- Ensure both the ON and CTS switches are in the ON position in the Dual SPST DIP Switch.

    ![Cryptoauth Trust Platform Development Kit CTS Switch in ON Position](./Images/SwitchPosition.jpg)

- Connect the micro USB port on the board to the computer using a micro USB cable.

## Opening the ECC608 AES Message Encryption Use Case

- Open [Trust Platform Design Suite](https://www.microchip.com/en-us/products/security/trust-platform/tpds) and navigate to Usecases Section.

- In the Use Case dropdown,search for "AES Message Encryption" and select "AES Message encryption" under the ATECC608-TFLXTLS group.

    ![Select AES Message Encryption](./Images/usecaseSelection.jpg)


- The ECC608 AES Message Encryption use case will open.

    ![ECC608 AES Message Encryption Usecase](./Images/usecase.jpg)

## Provisionig Usecases Resources

- From the Kit Dropdown, select the Cryptoauth Trust Platform Kit.

    ![Select Cryptoauth Trust Platform Kit](./Images/selectKit.jpg)

- Click on Proto Provision.

    ![Proto Provision](./Images/protoProvision.jpg)

- Select the Generate option to create and use a new Symmetric Key, or upload a user-specific Symmetric Key for  Mater Symmetric Key.
- Click on Proto Provision

    ![Proto Provision](./Images/generateResources.jpg)

- The necessary resources will be created at  `~/.trustplatform/aes_message_encryption`:
    - **slot_5_secret_key.h**: This file contains a 32-byte Master symmetric key, which is loaded into Slot 5, and it will be utilized to perform kdf operation to derive key in the Firmware project. 
    - **slot_5_secret_key.pem**: This file contains the generated symmetric key in PEM format.
    - **slot_6_secret_key.h**: This file contains the IO Protection key which is loaded into Slot 6.
    - **slot_6_secret_key.pem**: This file contains the IO Protection key which is loaded into Slot 6 in PEM format.
- Click on Yes in the pop-up to load resources onto ECC608.
- **Proto Provision Success Toast** will pop up after successfully loading resources, **Proto Provision Success** will be logged onto the terminal.

    ![Terminal Log](./Images/terminalLog.jpg)

## Build and Program Application
- Once the resources have been successfully loaded, open the Firmware Project by clicking on the Firmware button.

    ![Click on Firmware](./Images/openFirmware.jpg)

- The project **aes_msg_enc_ecc608** will open in the MPLABX IDE.
- Right-click on **aes_msg_enc_ecc608** and select "Set as Main Project".

    ![Set As Main Project](./Images/setMainProject.jpg)

- Click on "Make and Program Device".

    ![Click on Make and Program Device](./Images/makeProgram.jpg)

- After the programming process is complete, launch the Terminal application (e.g., Tera Term) on your computer.
- Connect to the Virtual COM port and configure the serial settings as follows:
    - Baud : 115200
    - Data : 8 Bits
    - Parity : None
    - Stop : 1 Bit
    - Flow Control : None
- Press the Reset button on Cryptoauth Trust Platform Development Kit
- Review the output message in the console:

   ![ECC608 AES Message Encryption Firmware Success](./Images/firmwareSuccess.png)

- Console displays a message stating the decrypted message matches the original message.

## Conclusion

The ECC608 AES Message Encryption use case demonstrates a secure method for encrypting messages by storing the master symmetric key within the ECC608 secure element. This ensures the key is never exposed, enhancing security. The guide provides detailed steps for setting up the hardware and software, provisioning resources, and programming the application. Successful execution and verification confirm the system's effectiveness in securely handling AES encryption. This use case highlights the importance of secure key storage and management in cryptographic operations.
