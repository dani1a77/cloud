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
![0](http://cloud.websputnik.su/git/img1.png)
4.	Далее переходим в раздел установки решений c marketplace в админке /bitrix/admin/partner_modules.php?lang=ru. И жмем напротив скопированного модуля - установить. ![0](http://cloud.websputnik.su/git/img2.png)


### Настройка модуля

1.	Сначала нужно создать новую платежную систему. Переходим «Магазин» -> “Платежные системы» /bitrix/admin/sale_pay_system.php?lang=ru
2.	Жем кнопку «Добавить платежную систему»
3.	В качестве обработчика выбираем CloudPayments (cloudpayment). 
Далее вводим:
- название
- описание и прочие поля заполняем по своему усмотрению. 
Жмем «Применить», чтобы появились настройки самой платежной системы.
4.	Далее переходим в раздел «Настройка обработчика ПС»
![0](http://cloud.websputnik.su/git/img3.png)
Заполняем:
- «Public ID»
- «Пароль для API», и выбираем «Тип схемы проведения платежей»
https://yadi.sk/i/ljItfaVa3SeNia
Остальные параметры заполняем на свое усмотрение. 

### Описание параметров модуля:
- **Success URL** - url на который будет переадресован пользователь после успешной оплаты заказа.
- **Fail URL** - url на который будет переадресован пользователь после неудачно оплаты заказа.
- **Язык виджета** - список доступных языков виджета оплаты заказа, который появляется когда пользователь нажимает кнопку "оплатить".
- **Использовать функционал онлайн касс** - при использование модуля онлайн касс, установив данный параметр, клиенту на почту будет приходить чек оплаты.
- **Тип схемы проведения платежей** - выбор схемы оплата платежной системы. Одностадийная оплата, или двухстадийна. При двухстадийной оплате требуется подтверждение оплаты заказа в административной части.
- **Статус возврата платежа** - в этом пункте выбирается какой статус заказа, отвечает за возврат платежа. Т.е. выбрав указанный в этом пункте статус, в заказе, будет выполнена функция возврата платежа через API cloudpayments.
- **Статус авторизации платежа (двухстадийные платежи)** - в этом пункте выбирнается какой статус заказа, будет установлен после оплаты пользователем при двухстадийной схеме платежей.
**Статус отмена авторизованного платежа (двухстадийные платежи)** - в этом пункте выбирается какой статус заказа, нужно выбрать в заказе, чтобы произвести отмену оплаты при двухстадийной схеме платежей, в момент когда оплата не подтверждена, а только авторизована. Подробнее о двухстадийной схеме оплат, можно прочитать у нас на сайте https://cloudpayments.ru/Docs/Integration#schemes





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
