Итак, были задания для самостоятельного исследования

1. Исследуйте сопоставление томов (volumes), так чтобы после работы контейнера mongodb данные, собранные через веб-интерфейс, были доступны в папке извне контейнера для дальнейшего повторного использования

2. Дополните конфигурацию docker-compose контейнером nginx так, чтобы nginx служил прокси запросов с порта 80 на тот, на котором работает наше API (например 3000)

Соответственно для пользователя запрос к API будет выглядеть более кратким:



1. Создаём скейлет с приложением-докером и подключаемся через .ssh

(если есть домен, например, ikoder.xyz, то оперативно изменяем его DNS-зону с учётом полученного IP, например 92.53.66.163)

```
Если нужно сгенерировать ключи

ssh-keygen -t rsa 

в конец публичного ключа добавляется имя_юзера@имя_компа

например vscale1@air

micro id_rsa.pub -  в настройках скейлета нужно найти SSH-ключи и добавить новый или при создании скейлета 
``` 

2. Выполняем

git clone -b mongorestvolume 'https://github.com/GossJS/mongorestdocker.git' /sites

3. Переходим в /sites/data и распаковываем templates_12112017.zip

4. Переходим в /sites и делаем docker-compose up

Теперь по корневому маршруту у нас будут доступны файлы из папки /sites/data для скачивания



---

Очень важно, что в файле docker-compose.yml мы связываем самый последний контейнер с предыдущими - это гарантирует, что они загрузятся раньше. Контейнер logger нужен только для отладки - чтобы увидеть, как он видит приходящие к нему запросы.

http://92.53.66.163/hello/my

даст logger /myapi/

http://92.53.66.163/hello/my/api/?param=cute

даст

logger /myapi//api/?param=cute


http://92.53.66.163/alldocs/templates?apiKey=ifna212ASFisfsjaAFFF

даст 

http://92.53.66.163:3000/api/templates?apiKey=ifna212ASFisfsjaAFFF

и таким образом список документов из БД

... и можно отправлять API-запросы используя этот адрес.

Если домен привязан к IP, то 

http://ikoder.xyz/alldocs/templates?apiKey=ifna212ASFisfsjaAFFF

и т.п.

---

Затем можно зазиповать получившееся содержимое папки  /data и использовать уже этот архив на следующей итерации. Или сделать экспорт.





В файле default.conf используются имена, которые docker помещает в файл hosts - это имена контейнеров. Без них пришлось бы использовать захардкоденные адреса (ikodder.xyz вместо logger и api).  
 

Следующая задача - обеспечить доступ по SSL/TLS




