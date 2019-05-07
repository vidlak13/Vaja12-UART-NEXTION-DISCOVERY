# Vaja12-UART-NEXTION-DISCOVERY
stevec z nextion displayom


ODGOVORI:
d.)  z0
g.) b0
3. b.) PC9 zelena LED, PC8 modra LED.
c.)f.) PA10 (Rx), PA9 (Tx). Rx iz displaya povežemo na tx na STMu in Tx povežemo z RXom.
d.)  ADC_IN10
4. e.) HAL_UART_Receive_DMA(&huart1, myRxData, 1);
f.) 

HAL_ADC_Start(&hadc);
  reading=AdcValue;
  potenciometer=HAL_GPIO_ReadPin(GPIOC, GPIO_PIN_0);
  if (HAL_ADC_PollForConversion(&hadc,5)==HAL_OK){
	  AdcValue=HAL_ADC_GetValue(&hadc);
  }
  HAL_ADC_Stop(&hadc);
  reading=AdcValue;
  reading/=23;
  myTxData[0]=(reading/100)+48;
  myTxData[1]=((reading/10)%10)+48+1;
  myTxData[2]=(reading%10)+48+2;
  myTxData[3]=0xff;
  myTxData[4]=0xff;
  myTxData[5]=0xff;
  if (reading>(reading_+1)||reading<(reading_-1)) {
  HAL_UART_Transmit(&huart1, (uint8_t *)"z0.val=", 7, 10);
  HAL_UART_Transmit(&huart1, myTxData, 6, 10);
  }
  HAL_Delay(10);
  -- Countinious pretvorba 

ASCII       Dvojiško     šestnajstiško  Decimalno
  0         0110000         30            48
  1         0110001         31            49
  2         0110010         32            50  
  3         0110011         33            51
  4         0110100         34            52  
  5         0110101         35            53
  6         0110110         36            54
  7         0110111         37            55
  8         0111000         38            56  
  9         0111001         39            57
  
  g.)
  void HAL_UART_RxCpltCallback(UART_HandleTypeDef*huart)
{
		UNUSED(huart);
		if (myRxData[0]==0xaa) HAL_GPIO_WritePin(GPIOC , GPIO_PIN_9 , GPIO_PIN_RESET);
		if (myRxData[0]==0xbb) HAL_GPIO_WritePin(GPIOC , GPIO_PIN_9 , GPIO_PIN_SET);
}

6. a.)
  if (AdcValue>2730)
	  HAL_GPIO_WritePin(GPIOC, GPIO_PIN_8, GPIO_PIN_SET);
  if (AdcValue<2730)
	  HAL_GPIO_WritePin(GPIOC, GPIO_PIN_8, GPIO_PIN_RESET);
    -------------------------------------------------------------------------
    
    Komentar:
    S pomočjo Nextion displaya in STM mikrokontrolerja smo na Nextion prikazovali (na števcu) stanje potenciometra in na displayu smo pritiskali tipko za vklop in izklop zelene LED diode. Ko vrednost števca preseže 120° se prižge modra LED. Program deluje brezhibno in brez zakasnitev. Največji problem so nama povzročale LED diode.
  
  
  
