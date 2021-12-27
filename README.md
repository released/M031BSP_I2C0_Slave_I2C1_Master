# M031BSP_I2C0_Slave_I2C1_Master
 M031BSP_I2C0_Slave_I2C1_Master

update @ 2021/12/27

1. initial I2C master (I2C1) and slave (I2C0) 

	slave : I2C0 : PC1 : SCL , PC0 : SDA
	
	master : I2C1 : PC5 : SCL , PC4 : SDA

##check define MASTER_I2C_USE_IRQ , MASTER_I2C_USE_POLLING , for different master I2C TX/RX flow

##In Master side , add UART RX IRQ , by using terminal command to test Master I2C command send to Slave

- In terminal (ex : teraterm) , when press 

- digit 1 : Master write customize data , digit 2 : Master request to read data from slave , 

- digit 9 : Master write then read

- digit 4 , 5  : write customize data , with customise register , multi data

##Slave behavior

- only interrupt available , 

- within the I2Cx_SlaveTRx , Insert I2Cx_Slave_StateMachine for customise the TX/RX data

- RX data will be save in g_u8FromMasterData array 

- RX length will be save in g_u8FromMasterLen

- RX flow stop at the "SLAVE_TRANSMIT_REPEAT_START_OR_STOP" inside the case "_state_RECEIVE_RX_" 

- Make sure to copy RX length if need to use later or it will be cleared at the "res == SLAVE_RECEIVE_ADDRESS_ACK" , check u8Temp

- TX data will be save in g_u8ToMasterData array 

- TX length will be save in g_u8ToMasterLen

- TX flow stop at the "SLAVE_TRANSMIT_DATA_NACK" inside the case "_state_TRANSMIT_TX_" 


2. below is press digit 1 , master send and slave receive data 

![image](https://github.com/released/M031BSP_I2C0_Slave_I2C1_Master/blob/main/Master_send.jpg)

3. below is press digit 2 , master receive , slave receive data and return data

![image](https://github.com/released/M031BSP_I2C0_Slave_I2C1_Master/blob/main/Master_read_Slave_receive_send.jpg.jpg)


