# hair
公关测试   开开开
void USART1_GPS_task(void *pvParameters)
{
	BaseType_t err=pdFALSE;
	printf("USART1_GPS_task Start......\r\n");
	
	while(1)
	{
		if(USART1_GPS_BS != NULL)
		{
			err = xSemaphoreTake(USART1_GPS_BS,portMAX_DELAY);		
			if(err==pdTRUE)											
			{
				printf("%s\r\n",USART1_RX_BUF);
				NMEA_GPRMC_Analysis();
			}
		}
		vTaskDelay(200);
	}
}  
void UART3_RECV_task(void *pvParameters)
{
	BaseType_t err=pdFALSE;
	printf("UART3_RECV_task Start......\r\n");
	while(1)
	{
		if(RCV_GW_BS != NULL)
		{
			err = xSemaphoreTake(RCV_GW_BS,portMAX_DELAY);		
			if(err==pdTRUE)											
			{
				if(mode_select == LORA_MODE)	//ÓëÍø¹ØÍ¨ÐÅµÄÊý¾Ý½âÎö
				{
					Usart3_Rcv_Gw_Data();
				}
				else if(mode_select == GPRS_MODE || mode_select == CONFIG_MODE || mode_select == WIFI_MODE)	//Óë·þÎñÆ÷Í¨ÐÅµÄÊý¾Ý½âÎö
				{
					Usart3_Rcv_Json_Data();
				}
			}
		}
		vTaskDelay(150);
	}
}
