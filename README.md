# 📦 Tc3_CRC Library

A comprehensive TwinCAT 3 CRC (Cyclic Redundancy Check) calculation library written in Structured Text (ST), with support for numerous standard CRC algorithms. 
---

## ✅ Features
- Supports most (all) used crc variants
- Supports streaming data by calling the update() method multiple time before finalizing
- The function block `CRC` can be initialized for any of the listed types below. 
It then uses a lookup table to efficiently compute the CRC using either normal or reflected bit logic.


## 🧠 Remarks and limitations

- The library can for now only be ran on a x64 bit runtime because of the LWORD (64bit) usage necessary for >CRC32
- Compiled with TwinCAT 4024.67 but tested on TwinCAT 4026.17


## 📦 Dependencies
* This library relies on [Tc3_AlgoInterfaces](https://www.github.com/kimro/Tc3_AlgoInterfaces) for the use of the generic IDigest interface.


## 🧪 Example

```iecst
VAR
    crc         : CRC(Tc3_Crc.E_CRC_Type.CRC_8_AUTOSAR); // Pass the required CRC type
    data        : ARRAY[1..9] OF BYTE := [1,2,3,4,5,6,7,8,9];
    result      : Tc3_Crc.U_8BYTEARRAY; // alias type from crc library
END_VAR

// if in-code CRC Type reinitialisation is necessary, use the init method
crc.reconfigure(Tc3_Crc.E_CRC_Type.CRC_8_AUTOSAR);      // reconfigures for new algorithm + init()
crc.init();                                             // initialization of calculation, reset current crc
crc.update(ADR(data), SIZEOF(data)-3);
crc.update(ADR(data)+6, SIZEOF(data)-6);	
crc.update(...);
crc.finalize(result.byteArray);                         //Returns the crc result in various result types in alias
```

## 🧠 Notes

- Tables are generated dynamically based on CRC parameters.
- Supports both normal and reflected CRC variants.
- Uses pre-initialized global data (`GVC_CRC`) for configuration.


## 🔢 Supported CRC Types

- `CRC_8_AUTOSAR`
- `CRC_8_BLUETOOTH`
- `CRC_8_CDMA2000`
- `CRC_8_DARC`
- `CRC_8_DVB_S2`
- `CRC_8_GSM_A`
- `CRC_8_GSM_B`
- `CRC_8_HITAG`
- `CRC_8_I_432_1`
- `CRC_8_I_CODE`
- `CRC_8_LTE`
- `CRC_8_MAXIM_DOW`
- `CRC_8_MIFARE_MAD`
- `CRC_8_NRSC_5`
- `CRC_8_OPENSAFETY`
- `CRC_8_ROHC`
- `CRC_8_SAE_J1850`
- `CRC_8_SMBUS`
- `CRC_8_TECH_3250`
- `CRC_8_WCDMA`
- `CRC_16_ARC`
- `CRC_16_CDMA2000`
- `CRC_16_CMS`
- `CRC_16_DDS_110`
- `CRC_16_DECT_R`
- `CRC_16_DECT_X`
- `CRC_16_DNP`
- `CRC_16_EN_13757`
- `CRC_16_GENIBUS`
- `CRC_16_GSM`
- `CRC_16_IBM_3740`
- `CRC_16_IBM_SDLC`
- `CRC_16_ISO_IEC_14443_3_A`
- `CRC_16_KERMIT`
- `CRC_16_LJ1200`
- `CRC_16_MAXIM_DOW`
- `CRC_16_MCRF4XX`
- `CRC_16_MODBUS`
- `CRC_16_NRSC_5`
- `CRC_16_OPENSAFETY_A`
- `CRC_16_OPENSAFETY_B`
- `CRC_16_PROFIBUS`
- `CRC_16_RIELLO`
- `CRC_16_SPI_FUJITSU`
- `CRC_16_T10_DIF`
- `CRC_16_TELEDISK`
- `CRC_16_TMS37157`
- `CRC_16_UMTS`
- `CRC_16_USB`
- `CRC_16_XMODEM`
- `CRC_24_BLE`
- `CRC_24_FLEXRAY_A`
- `CRC_24_FLEXRAY_B`
- `CRC_24_INTERLAKEN`
- `CRC_24_LTE_A`
- `CRC_24_LTE_B`
- `CRC_24_OPENPGP`
- `CRC_24_OS_9`
- `CRC_32_AIXM`
- `CRC_32_AUTOSAR`
- `CRC_32_BASE91_D`
- `CRC_32_BZIP2`
- `CRC_32_CD_ROM_EDC`
- `CRC_32_CKSUM`
- `CRC_32_ISCSI`
- `CRC_32_ISO_HDLC`
- `CRC_32_JAMCRC`
- `CRC_32_MEF`
- `CRC_32_MPEG_2`
- `CRC_32_XFER`
- `CRC_40_GSM`
- `CRC_64_ECMA_182`
- `CRC_64_GO_ISO`
- `CRC_64_MS`
- `CRC_64_WE`
- `CRC_64_XZ`

Source: [reveng CRC Catalogue](https://reveng.sourceforge.io/crc-catalogue/all.htm)


## ⚖️ License-related information

Attribution to the work of tanel312.
This library is derived work based on https://github.com/tanel312/CRCcalculation_Library by tanel312 that was released under GNU General Public License v3.
 
