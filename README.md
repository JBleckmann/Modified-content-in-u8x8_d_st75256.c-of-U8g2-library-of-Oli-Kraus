# Modified-content-in-u8x8_d_st75256.c-of-U8g2-library-of-Oli-Kraus

The file u8x8_d_st75256c contents modified code from line 369 in the origin file. The file inits ST75161 instead of ST75256 to drive circle display Winstar WO128128A2-TFH#
The origin files is at https://github.com/olikraus/u8g2/blob/1b656cbd5d61d5a907a0f9f32e3b48fd5e2fc3cf/csrc/u8x8_d_st75256.c

![WO128128A2-TFH# SPI](https://user-images.githubusercontent.com/32862272/101745242-6dcf3400-3acb-11eb-9072-26b36f8badfa.jpg)

The Winstar WO128128A2-TFH# offers 3 options for interface, 8080, I2C, SPI. Below description is for 4-Wire SPI with Chip-Select. Connection to Reset is recommended. Wiring for SPI:

![Wiring for SPI](https://user-images.githubusercontent.com/32862272/101778754-91f33b00-3af4-11eb-9dfc-77744721851d.PNG)

Interface selection pins on board all to Low

![Interface selection spec](https://user-images.githubusercontent.com/32862272/101779084-147bfa80-3af5-11eb-9717-3faac550d822.PNG)

![Interface selection board](https://user-images.githubusercontent.com/32862272/101778998-f7472c00-3af4-11eb-84ce-9b50d19d50a5.PNG)
