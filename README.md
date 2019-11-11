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
