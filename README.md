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
5. Чтобы модуль корректно работал, нужно внести ряд изменений в настройки модуля, а также настроить работу вебхуков в личном кабинете - https://merchant.cloudpayments.ru/Account/Login. Настройки модуля и настройки вебхуков описаны ниже.

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
![0](http://cloud.websputnik.su/git/slide11.png)
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
- **Выберите НДС на доставку, если необходимо** - в данном разделе можно установить размер ндс, с привязкой к добавленным на сайте службам доставки.


### Настройка вебхуков:

Для корректной работы модуля, а именно подтверждения оплаты, подтверждения авторизации и прочих действий, нужно прописать правильные url в настройках вебхуков. 
Так как  настройка ЧПУ(Семантический URL) может быть отличной от параметра по умолчаню, то для корректной настройки вебхуков лучше всего будет использовать след. способ:
Для настройки вебхуков:
1) Авторизуемся в личном кабинете по ссылке https://merchant.cloudpayments.ru/Account/Login
2) Переходим в "Сайты"  
![0](http://cloud.websputnik.su/git/img4.png)
3) Добавляем свой сайт, если еще не добавили и переходим в настройки
![0](http://cloud.websputnik.su/git/img5.png)
3) Далее жмем еще раз настройки
![0](http://cloud.websputnik.su/git/img6.png)

Напротив каждого хука копируем линк ниже для соответсвующего вебхука:

* (Check) 		#SITE_URL#/bitrix/tools/sale_ps_result.php?action=check
* (Fail) 		#SITE_URL#/bitrix/tools/sale_ps_result.php?action=fail
* (Pay) 		#SITE_URL#/bitrix/tools/sale_ps_result.php?action=pay
* (Confirm)		#SITE_URL#bitrix/tools/sale_ps_result.php?action=confirm
* (Refund)		#SITE_URL#/bitrix/tools/sale_ps_result.php?action=refund

Где #SITE_URL# - адрес сайта. Например: http://domain.ru


### Двухстадийная оплата

Двухстадийная оплата подразумевает использование двух команд: отдельно на авторизацию, отдельно на списание. После успешной авторизации, сумма операции будет блокирована на счету держателя, то есть он не сможет ей воспользоваться. Далее у ТСП есть до 30 дней в зависимости от типа карты для подтверждения операции, после чего произойдет списание денег. Если операцию не подтвердить в течение этого времени — она будет автоматически отменена. Подтверждать можно как всю сумму авторизации, так и часть.

Как правило, двухстадийная схема используется для получения депозита с плательщика, например, в прокатных компаниях или отелях.


В зависимости от настройки, система может автоматически выполнять подтверждение двустадийных платежей через указанное количество дней.

Для того чтобы включить двухстадийную оплату нужно зайти в настройки модуля и в "Тип схемы проведения платежей" выбрать "Двухстадийная оплата". После чего платежная система будет работать по следующей схеме:
1) Клиент оплачивает на сайте заказа
2) Заказ переходит в статус "Авторизован"
и в данный момент оплата считается "авторизованной" и требует подтверждения администратором в административной части.
3) Для этого переходим в редактирования соответствующего заказа. И меняем текущий статус заказа на новый. Выбранный в этом пункте настроек модуля
![0](http://cloud.websputnik.su/git/img7.png)
4) После того как будет получен ответ от cloudpayments (если вы настроили вебхук confirm), об успешном подтверждение, заказ будет считается оплачен. И статус заказа перейдет в "оплачен, формируется к отправке".


### Двухстадийная оплата - отмена авторизованного платежа

Чтобы отменить авторизованную, но не подтвержденную оплату. Нужно перейти в редактирование заказа и в статусе заказа выбрать статус выбранный в настройках модуля
![0](http://cloud.websputnik.su/git/img8.png)
После чего будет отправлен void запрос на отмену оплаты. 


### Отмена оплаченного заказа

Чтобы отменить оплаченный заказ. Нужно перейти в редактирование заказа и в статусе заказа выбрать статус выбранный в настройках модуля
![0](http://cloud.websputnik.su/git/img9.png)
После чего будет отправлен refund запрос на отмену оплаты. Также отмена оплаты будет произведена автоматически, если будет отменен или удален заказ в ЛК сайта или в редактирование заказа. 


### Заказы в статусе "возврат"

Если заказа в статусе возврат, кнопки оплатить виджета не будет, ,а вместо нее будет выводиться фраза
![0](http://cloud.websputnik.su/git/img12.png)
Текст можно изменить тут
/bitrix/php_interface/include/sale_payment/cloudpayment/template/lang/ru/template.php
В личном кабинете пользователя может выводиться кнопка "оплатить" компонента, но при нажатие кнопки будет выводиться фраза описанная выше. 
Кнопку оплаты битрикса можно удалить в шаблоне списка заказов
sale.personal.order.list в случае если используется стандартный компонент битрикса.




### Прочие настройки

При двухстадийной схеме оплаты, и использование дефолтного личного кабинета пользователя на сайте. Может возникнуть ситуация, что заказа оплачен пользователем (авторизована оплата), но не подтверждена администратором сайта. И фактически битрикс такой заказ считает не оплаченым, и выводит в личном кабинете кнопку оплаты. Пример:
![0](http://cloud.websputnik.su/git/img10.png)
Виджет модуля Cloudpayments конечно такой заказа повторно оплатить не даст, и при нажатие оплаты. Выведет текст, что заказ уже оплачен и требует подтверждения
![0](http://cloud.websputnik.su/git/img11.png)
Данный текст можно поменять тут /bitrix/php_interface/include/sale_payment/cloudpayment/template/lang/ru/template.php

Кнопку оплаты битрикса можно удалить в шаблоне списка заказов
sale.personal.order.list в случае если используется стандартный компонент битрикса.
