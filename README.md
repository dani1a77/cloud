# CloudPayments модуль для Bitrix
Модуль позволит с легкостью добавить на ваш сайт оплату банковскими картами через платежный сервис CloudPayments. 
Для корректной работы модуля необходима регистрация в сервисе.

### Совместимость:
Подходящие редакции:«Малый бизнес», «Бизнес», «Корпоративный портал», «Энтерпрайз»

### Возможности:  
• Одностадийная схема оплаты;  
• Двухстадийная схема оплаты;  
• Отмена, подтверждение и возврат платежей из ЛК CMS;    
• Отправка чеков по email;



### Установка через bitrix marketplace

Заходим на страничку модуля в marketplace http://marketplace.1c-bitrix.ru/solutions/cloudpayments.cloudpayment/, жмем установить, указываем url сайта, нас перебросит на сайт. После чего нужно авторизоваться под админом, и скачать и установить модуль.

### Ручная установка

1.	Копируем архив с github. На ftp создаем папку /bitrix/modules/cloudpayments.cloudpayment
2.	В папку копируем все содержимое из архивной папки \cloudpayments.cloudpayment\.last_version\ 
3.	Итого в папке /bitrix/modules/cloudpayments.cloudpayment должны быть следующие файлы 
![8](https://github.com/dani1a77/cloud/tree/master/images/img1.png)
4.	Далее переходим в раздел установки решений c marketplace в админке /bitrix/admin/partner_modules.php?lang=ru. И жмем напротив скопированного модуля ![]({{site.baseurl}}/https://yadi.sk/i/S1Gm9jkE3Rb6Wf) установить


### Настройка вебхуков:

Так как  настройка ЧПУ(Семантический URL) может быть отличной от параметра по умолчаню,
 то для корректной настройки вебхуков лучше всего будет использовать след. способ:

Копируем линк ниже для соответсвующего вебхука:

* (Check) 		index.php?option=com_virtuemart&view=pluginresponse&task=pluginresponsereceived&cloudpayments_check
* (Pay) 		index.php?option=com_virtuemart&view=pluginresponse&task=pluginresponsereceived&cloudpayments_pay
* (Confirm)		index.php?option=com_virtuemart&view=pluginresponse&task=pluginresponsereceived&cloudpayments_confirm
* (Refund)		index.php?option=com_virtuemart&view=pluginresponse&task=pluginresponsereceived&cloudpayments_refund

Открываем свой сайт, например,  http://**yourdomain.name** или https://**yourdomain.name**, где **yourdomain.name** - доменное имя сайта.

В итоге, должно получится что-то вроде:
http://**yourdomain.name**/index.php?option=com_virtuemart&view=pluginresponse&task=pluginresponsereceived&cloudpayments_check

Открыв его, вы увидите ответ:
![8](https://github.com/cloudpayments/CMS-Joomla-VirtueMart-CP/blob/master/Images/8.PNG)
Если все верно, то настройки ЧПУ преобразуют ссылку,
например, в http://**yourdomain.name**/ru/?option=com_virtuemart&view=pluginresponse&task=pluginresponsereceived&cloudpayments_check

Преобразованная ссылка  будет являться необходимым URL для check-уведомления в ЛК CloudPayments.
Аналогичным образом настройте остальные вебхуки.

![9](https://github.com/cloudpayments/CMS-Joomla-VirtueMart-CP/blob/master/Images/9.PNG)


Внимание!!! Убедитесь, что используемые валюты в глобальных настройках VirtueMart'а,
 а именно их трехбуквенные наименования совпадают с  параметрами, поддерживающимися сервисом отправки чеков.
https://cloudpayments.ru/Docs/Directory#currencies  
Так же будьте внимательны с настройками НДС.
