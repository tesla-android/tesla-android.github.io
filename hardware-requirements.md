## Hardware requirements (2022.38.1)

Note: MCU 1 (cars previous to March 2018 without an infotainment upgrade) are not supported, as the built-in browser is out of date and too slow.

#### Older versions

If you wish to run the legacy dual board configuration check out this link: 
- [Hardware requirements (dual board stack)](/hardware-requirements-dual-board)

| Component | Description |
|--------|--------|
| Raspberry Pi 4 | Main device for running Android. 4GB of RAM recommended |
| Geekworm TC358743XBG HDMI-CSI-2| Required for video capture |
| Short microHDMI to HDMI cable | Connects Android video out to HDMI to CSI adapter |
| Argon Mini Fan | Cooling for Raspberry Pi 4, after testing multiple solutions I can only recommend this one.  |

### Optional

| Component | Description |
|--------|--------|
| Open housing for Raspberry Pi 4  | Makes cable management easy, allows all the hardware to fit into the center console |
| CarlinKit CPC200-Autokit, CPC200-CCPA | If you intend to use any form of CarPlay or Android Auto (wireless or wired). For wireless Android Auto order the new model: CPC200-CCPA |
| Huawei E3372(Europe), Alcatel IK41VE1(Europe), Alcatel IK41UC(North America) | Optional LTE modem, can be replaced with a different model that works on Raspbian out of the box. The modem is required if you plan on using Premium Connectivity features like online routing alongside Tesla Android. |

## Notes

Geekworm TC358743XBG HDMI-CSI-2 is the next component that will be removed from the hardware requirements. 
