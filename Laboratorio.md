# Startup.c com tabela de vetores adicionados

#include <stdint.h>

 /****************************************************************************
 * Pre-processor Definitions
 ****************************************************************************/

#define SRAM_START  0x20000000U                  /* Inicio da SRAM CORTEX-M */
#define SRAM_SIZE   (128U * 1024U)               /* Tam. SRAM STM32F411 128K */
#define SRAM_END    ((SRAM_START) + (SRAM_SIZE)) /* Final da SRAM STM32F411 */

#define STACK_START SRAM_END                     /* Inicio da Stack */

/****************************************************************************
 * Private Function Prototypes
 ****************************************************************************/

int main(void);

/* Prototipos de funcoes para as System Exceptions */

void reset_handler     (void);
void nmi_handler       (void) __attribute__ ((weak, alias("default_handler")));
void hardfault_handler (void) __attribute__ ((weak, alias("default_handler")));
void memmanage_handler (void) __attribute__ ((weak, alias("default_handler")));
void busfault_handler  (void) __attribute__ ((weak, alias("default_handler")));
void usagefault_handler(void) __attribute__ ((weak, alias("default_handler")));
void svc_handler       (void) __attribute__ ((weak, alias("default_handler")));
void debugmon_handler  (void) __attribute__ ((weak, alias("default_handler")));
void pendsv_handler    (void) __attribute__ ((weak, alias("default_handler")));
void systick_handler   (void) __attribute__ ((weak, alias("default_handler")));
void wwdg_handler   (void) __attribute__ ((weak, alias("default_handler")));
void pvd_handler   (void) __attribute__ ((weak, alias("default_handler")));
void tampstamp_handler   (void) __attribute__ ((weak, alias("default_handler")));
void rtcwkup_handler   (void) __attribute__ ((weak, alias("default_handler")));
void flash_handler   (void) __attribute__ ((weak, alias("default_handler")));
void rcc_handler   (void) __attribute__ ((weak, alias("default_handler")));
void exti0_handler   (void) __attribute__ ((weak, alias("default_handler")));
void exti1_handler   (void) __attribute__ ((weak, alias("default_handler")));
void exti2_handler   (void) __attribute__ ((weak, alias("default_handler")));
void exti3_handler   (void) __attribute__ ((weak, alias("default_handler")));
void exti4_handler   (void) __attribute__ ((weak, alias("default_handler")));
void dma1stream0_handler   (void) __attribute__ ((weak, alias("default_handler")));
void dma1stream1_handler   (void) __attribute__ ((weak, alias("default_handler")));
void dma1stream2_handler   (void) __attribute__ ((weak, alias("default_handler")));
void dma1stream3_handler   (void) __attribute__ ((weak, alias("default_handler")));
void dma1stream4_handler   (void) __attribute__ ((weak, alias("default_handler")));
void dma1stream5_handler   (void) __attribute__ ((weak, alias("default_handler")));
void dma1stream6_handler   (void) __attribute__ ((weak, alias("default_handler")));
void adc_handler   (void) __attribute__ ((weak, alias("default_handler")));
void exti9_5_handler   (void) __attribute__ ((weak, alias("default_handler")));
void TIM1_BRK_TIM9_handler   (void) __attribute__ ((weak, alias("default_handler")));
void TIM1_UP_TIM10_handler   (void) __attribute__ ((weak, alias("default_handler")));
void TIM1_TRG_COM_TIM11_handler   (void) __attribute__ ((weak, alias("default_handler")));
void TIM1_CC_handler   (void) __attribute__ ((weak, alias("default_handler")));
void TIM2_handler   (void) __attribute__ ((weak, alias("default_handler")));
void TIM3_handler   (void) __attribute__ ((weak, alias("default_handler")));
void TIM4_handler   (void) __attribute__ ((weak, alias("default_handler")));
void I2C1_EV_handler   (void) __attribute__ ((weak, alias("default_handler")));
void I2C1_ER_handler   (void) __attribute__ ((weak, alias("default_handler")));
void I2C2_EV_handler   (void) __attribute__ ((weak, alias("default_handler")));
void I2C2_ER_handler   (void) __attribute__ ((weak, alias("default_handler")));
void SPI1_handler   (void) __attribute__ ((weak, alias("default_handler")));
void SPI2_handler   (void) __attribute__ ((weak, alias("default_handler")));
void USART1_handler   (void) __attribute__ ((weak, alias("default_handler")));
void USART2_handler   (void) __attribute__ ((weak, alias("default_handler")));
void EXTI15_10_handler   (void) __attribute__ ((weak, alias("default_handler")));
void RTC_Alarm_handler   (void) __attribute__ ((weak, alias("default_handler")));
void OTG_FS_WKUP_handler   (void) __attribute__ ((weak, alias("default_handler")));
void DMA1_Stream7_handler   (void) __attribute__ ((weak, alias("default_handler")));
void SDIO_handler   (void) __attribute__ ((weak, alias("default_handler")));
void TIM5_handler   (void) __attribute__ ((weak, alias("default_handler")));
void SPI3_handler   (void) __attribute__ ((weak, alias("default_handler")));
void DMA2_Stream0_handler   (void) __attribute__ ((weak, alias("default_handler")));
void DMA2_Stream1_handler   (void) __attribute__ ((weak, alias("default_handler")));
void DMA2_Stream2_handler   (void) __attribute__ ((weak, alias("default_handler")));
void DMA2_Stream3_handler   (void) __attribute__ ((weak, alias("default_handler")));
void DMA2_Stream4_handler   (void) __attribute__ ((weak, alias("default_handler")));
void OTG_FS_handler   (void) __attribute__ ((weak, alias("default_handler")));
void DMA2_Stream5_handler   (void) __attribute__ ((weak, alias("default_handler")));
void DMA2_Stream6_handler   (void) __attribute__ ((weak, alias("default_handler")));
void DMA2_Stream7_handler   (void) __attribute__ ((weak, alias("default_handler")));
void USART6_handler   (void) __attribute__ ((weak, alias("default_handler")));
void I2C3_EV_handler   (void) __attribute__ ((weak, alias("default_handler")));
void I2C3_ER_handler   (void) __attribute__ ((weak, alias("default_handler")));
void FPU_handler   (void) __attribute__ ((weak, alias("default_handler")));
void SPI4_handler   (void) __attribute__ ((weak, alias("default_handler")));
void SPI5_handler   (void) __attribute__ ((weak, alias("default_handler")));

 /****************************************************************************
 * External Data
 ****************************************************************************/

/* Variaveis exportadas pelo linker script */

extern uint32_t _sdata;     /* Inicio da secao .data */
extern uint32_t _edata;     /* Fim da secao .data */
extern uint32_t _la_data;   /* Origem da secao .data na FLASH */

extern uint32_t _sbss;      /* Inicio da secao .bss */
extern uint32_t _ebss;      /* Fim da secao .bss */

/****************************************************************************
 * Private Data
 ****************************************************************************/

/* Tabela de Vetores de Interrupção */

uint32_t vectors[] __attribute__((section(".isr_vectors"))) =
{
  STACK_START,                            /* 0x0000 0000 */
  (uint32_t)reset_handler,                /* 0x0000 0004 */
  (uint32_t)nmi_handler,                  /* 0x0000 0008 */
  (uint32_t)hardfault_handler,            /* 0x0000 000c */
  (uint32_t)memmanage_handler,            /* 0x0000 0010 */
  (uint32_t)busfault_handler,             /* 0x0000 0014 */
  (uint32_t)usagefault_handler,           /* 0x0000 0018 */
  0,                                      /* 0x0000 001c */
  0,                                      /* 0x0000 0020 */
  0,                                      /* 0x0000 0024 */
  0,                                      /* 0x0000 0028 */
  (uint32_t)svc_handler,                  /* 0x0000 002c */
  (uint32_t)debugmon_handler,             /* 0x0000 0030 */
  0,                                      /* 0x0000 0034 */
  (uint32_t)pendsv_handler,               /* 0x0000 0038 */
  (uint32_t)systick_handler,              /* 0x0000 003c */
  (uint32_t)wwdg_handler,
  (uint32_t)pvd_handler, 
  (uint32_t)tampstamp_handler,
  (uint32_t)rtcwkup_handler,
  (uint32_t)flash_handler,
  (uint32_t)rcc_handler,
  (uint32_t)exti0_handler,
  (uint32_t)exti1_handler,
  (uint32_t)exti2_handler,
  (uint32_t)exti3_handler,
  (uint32_t)exti4_handler,
  (uint32_t)dma1stream0_handler ,
  (uint32_t)dma1stream1_handler ,
  (uint32_t)dma1stream2_handler ,
  (uint32_t)dma1stream3_handler ,
  (uint32_t)dma1stream4_handler ,
  (uint32_t)dma1stream5_handler ,
  (uint32_t)dma1stream6_handler, 
  (uint32_t)adc_handler,
  (uint32_t)exti9_5_handler,
  (uint32_t)TIM1_BRK_TIM9_handler,
  (uint32_t)TIM1_UP_TIM10_handler,
  (uint32_t)TIM1_TRG_COM_TIM11_handler,
  (uint32_t)TIM1_CC_handler,
  (uint32_t)TIM2_handler,
  (uint32_t)TIM3_handler,
  (uint32_t)TIM4_handler,
  (uint32_t)I2C1_EV_handler,
  (uint32_t)I2C1_ER_handler,
  (uint32_t)I2C2_EV_handler,
  (uint32_t)I2C2_ER_handler,
  (uint32_t)SPI1_handler,
  (uint32_t)SPI2_handler,
  (uint32_t)USART1_handler,
  (uint32_t)USART2_handler,
  (uint32_t)EXTI15_10_handler,
  (uint32_t)RTC_Alarm_handler ,
  (uint32_t)OTG_FS_WKUP_handler,
  (uint32_t)DMA1_Stream7_handler,
  (uint32_t)SDIO_handler,
  (uint32_t)TIM5_handler,
  (uint32_t)SPI3_handler,
  (uint32_t)DMA2_Stream0_handler,
  (uint32_t)DMA2_Stream1_handler,
  (uint32_t)DMA2_Stream2_handler,
  (uint32_t)DMA2_Stream3_handler,
  (uint32_t)DMA2_Stream4_handler,
  (uint32_t)OTG_FS_handler,
  (uint32_t)DMA2_Stream5_handler,
  (uint32_t)DMA2_Stream6_handler ,
  (uint32_t)DMA2_Stream7_handler ,
  (uint32_t)USART6_handler,
  (uint32_t)I2C3_EV_handler,
  (uint32_t)I2C3_ER_handler,
  (uint32_t)FPU_handler ,
  (uint32_t)SPI4_handler,
  (uint32_t)SPI5_handler,
  
};

/****************************************************************************
 * Private Functions
 ****************************************************************************/

void reset_handler(void)
{
  uint32_t i; 

  /* Copia a secao .data para a RAM */
   
  uint32_t size = (uint32_t)&_edata - (uint32_t)&_sdata;
  uint8_t *pDst = (uint8_t*)&_sdata;                      /* SRAM */
  uint8_t *pSrc = (uint8_t*)&_la_data;                    /* FLASH */
  
  for(i = 0; i < size; i++)
  {
    *pDst++ = *pSrc++;
  }

  /* Preenche a secao .bss com zero */

  size = (uint32_t)&_ebss - (uint32_t)&_sbss;
  pDst = (uint8_t*)&_sbss;
  for(i = 0 ; i < size; i++)
  {
    *pDst++ = 0;
  }

  /* Chama a funcao main() */

  main();
}

void default_handler(void)
{
  while(1){};
}



# Makefile com script capaz de gerar os arquivos objetos realocáveis e gerenciar automaticamente as dependências dos arquivos fonte do projeto

CC = arm-none-eabi-gcc
RM = rm -rf
OBJDIR = build
DEPDIR = .deps

SRCS = startup.c \
        main.c

CFLAGS = -g -mcpu=cortex-m4 -mthumb -Wall -O0
DEPFLAGS = -MMD -MP -MF $(DEPDIR)/$*.d

OBJS = $(patsubst %, $(OBJDIR)/%.o, $(basename $(SRCS)))
$(shell mkdir -p $(dir $(OBJS)) > /dev/null)
DEPS = $(patsubst %, $(DEPDIR)/%.d, $(basename $(SRCS)))
$(shell mkdir -p $(dir $(DEPS)) > /dev/null)
all: $(OBJS)
$(OBJDIR)/%.o: %.c $(DEPDIR)/%.d
	$(CC) -c $(CFLAGS) $(DEPFLAGS) $< -o $@
$(DEPS):
-include $(DEPS)

.PHONY: clean
clean:
	$(RM) $(OBJDIR) $(DEPDIR)
