# Modified-content-in-u8x8_d_st75256.c-of-U8g2-library-of-Oli-Kraus

# This files contents modified code from line 369 in the origin file. The file init ST75161 instead of ST75256 to drive circle display Winstar WO128128A2-TFH#


# Modification:
/*=============================================*/
/* WO256X128, https://github.com/olikraus/u8g2/issues/891  */

static const u8x8_display_info_t u8x8_st75256_wo256x128_display_info =
{                                     // Modified for ST75161 Winstar WO128128A2TFH#
  /* chip_enable_level = */ 0,
  /* chip_disable_level = */ 1,
  
  /* post_chip_enable_wait_ns = */ 20,
  /* pre_chip_disable_wait_ns = */ 20,
  /* reset_pulse_width_ms = */ 5, 	
  /* post_reset_wait_ms = */ 5, 		/**/
  /* sda_setup_time_ns = */ 20,		/* */
  /* sck_pulse_width_ns = */ 40,	/*  */
  /* sck_clock_hz = */ 4000000UL,	/* since Arduino 1.6.0, the SPI bus speed in Hz. Should be  1000000000/sck_pulse_width_ns */
  /* spi_mode = */ 0,		/* active high, rising edge */
  /* i2c_bus_clock_100kHz = */ 4,	/* 400KHz */
  /* data_setup_time_ns = */ 15,
  /* write_pulse_width_ns = */ 70,	
  /* tile_width = */ 32,
  /* tile_hight = */ 16,
  /* default_x_offset = */ 0,	/* must be 0, because this is checked also for normal mode */
  /* flipmode_x_offset = */ 0,		/* used as y offset */
  /* pixel_width = */ 128,
  /* pixel_height = */ 128
};


static const uint8_t u8x8_d_st75256_wo256x128_init_seq[] = {
  U8X8_START_TRANSFER(),             	/* enable chip, delay is part of the transfer start */

  U8X8_C( 0x030 ),				// Extension Command 1
  U8X8_C( 0x06E ),			
  
  U8X8_C( 0x031 ),			    // Extension Command 2
  U8X8_CA( 0x0d7, 0x09f),	    // Set auto-read instruction, Disable Auto Read
  
  U8X8_CA( 0x0e0 ,0x000),      // Enable OTP Read
  U8X8_DLY(10),
  
  U8X8_C( 0x0e3 ),              // OTP Read
  U8X8_DLY(20),
  U8X8_C(0xe1),          // OTP Control Out
  
  U8X8_C(0x30),          // Extension Command 1
  U8X8_C(0x94),          // Sleep Out
  U8X8_C(0xae),          // Display OFF  
  U8X8_DLY(50),
    
  U8X8_CA(0x20,0x0b ),          //Power Control VB, VR,VF All ON
  
  U8X8_CAA(0x81, 0x0d,0x04 ),   // Set Vop = 14V
  
  U8X8_C(0x31),            // Extension Command 2
  U8X8_C(0x20),           // Set Gray Scale Level
  U8X8_A(0x00),
  U8X8_A(0x00),
  U8X8_A(0x00),
  U8X8_A(0x00),
  U8X8_A(0x00),
  U8X8_A(0x00),
  U8X8_A(0x00),
  U8X8_A(0x00),
  U8X8_A(0x1f),
  U8X8_A(0x00),
  U8X8_A(0x00),
  U8X8_A(0x1f),
  U8X8_A(0x1f),
  U8X8_A(0x1f),
  U8X8_A(0x00),
  U8X8_A(0x00),

  U8X8_CAAA(0x32, 0x00, 0x01, 0x02),  // Analog Circuit SetBooster, Efficiency = Level 1, Bias=1/12

  U8X8_CA(0x51, 0xfb),          // Booster Level x10

  U8X8_CAAAA(0xf0, 0x02, 0x08, 0x0f, 0x18),  // frame rate setting

  U8X8_C(0x30),                 // Extension Command 2
  U8X8_CA( 0x0f0, 0x010 ),		/* monochrome mode  = 0x010*/

  U8X8_CAAA(0xca, 0x00, 0x87, 0x00),     /* display control, 3 args follow  */
  /* 0x00: no clock division, 0x04: divide clock */
  /* 1/136 duty value from the DS example code */
  /* Line cycles in a frame */

  U8X8_CA(0xbc, 0x00),      /*Column and page direction  */
  U8X8_C(0x0C),       //data format 0C LSB top

  U8X8_C(0xa6),       //Normal Display
  
  U8X8_C(0x31),       //Extension Command 2
  U8X8_C(0x40),       //Internal Power Supply

  U8X8_C(0x30),
  U8X8_C( 0x077 ),				/* Enable ICON RAM */
  U8X8_CAA(0x15, 0x00, 0x9F),		/* col range */
  U8X8_C( 0x76 ),				/* Disable ICON RAM */
  U8X8_CAA(0x75, 0x00, 0x10),		/* row range */
  
  U8X8_CAA(0x15, 0x00, 0x9F),      // Column Address Setting SEG0 -> SEG159
  U8X8_CAA(0x75, 0x00, 0x10),       // Row Address Setting,  16 Page address

//  U8X8_C(0x30),      
//  U8X8_CAA(0x15, 0x00, 0x7f),         // Column Address Setting 135
  
  U8X8_C(0xaf),                 // Display ON
  
  U8X8_END_TRANSFER(),             	/* disable chip */
  U8X8_END()             			/* end of sequence */
};


